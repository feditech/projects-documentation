# Security Policy and Best Practices

This document outlines security considerations, best practices, and policies for HexMate.

## Table of Contents

- [Reporting Security Issues](#reporting-security-issues)
- [Security Architecture](#security-architecture)
- [Authentication Security](#authentication-security)
- [Data Protection](#data-protection)
- [API Security](#api-security)
- [Frontend Security](#frontend-security)
- [Deployment Security](#deployment-security)
- [Security Best Practices](#security-best-practices)
- [Compliance](#compliance)
- [Security Checklist](#security-checklist)

## Reporting Security Issues

### How to Report

**DO NOT** create public GitHub issues for security vulnerabilities.

Instead, report security issues privately:

1. **Email:** Contact the repository maintainers via GitHub or the issue tracker
2. **Include:**
   - Description of the vulnerability
   - Steps to reproduce
   - Potential impact
   - Suggested fix (if any)
   - Your contact information

### Response Timeline

- **Acknowledgment:** Within 48 hours
- **Initial Assessment:** Within 1 week
- **Resolution Timeline:** Based on severity
  - Critical: 7 days
  - High: 14 days
  - Medium: 30 days
  - Low: 60 days

### Disclosure Policy

- Security issues will be fixed before public disclosure
- Credit will be given to reporters (if desired)
- CVE will be requested for significant vulnerabilities
- Security advisories will be published after fixes are deployed

## Security Architecture

### Defense in Depth

HexMate implements multiple layers of security:

```
┌─────────────────────────────────────┐
│   User Browser                       │
│   - HTTPS enforced                   │
│   - Content Security Policy          │
│   - XSS Protection                   │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│   Frontend Application               │
│   - Input validation                 │
│   - Output encoding                  │
│   - Token management                 │
│   - Secure storage                   │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│   API Layer                          │
│   - Authentication                   │
│   - Authorization                    │
│   - Rate limiting                    │
│   - Request validation               │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│   Backend Services                   │
│   - Business logic security          │
│   - Data access control              │
│   - Audit logging                    │
└─────────────────────────────────────┘
```

### Security Principles

1. **Least Privilege:** Users have minimum necessary permissions
2. **Defense in Depth:** Multiple security layers
3. **Fail Securely:** Failures default to secure state
4. **Complete Mediation:** Every access is checked
5. **Open Design:** Security through design, not obscurity
6. **Separation of Duties:** Critical operations require multiple approvals
7. **Audit Trail:** All security-relevant events are logged

## Authentication Security

### Token-Based Authentication

**JWT Implementation:**
```typescript
// Access Token
{
  "sub": "user@example.com",
  "iat": 1638360000,
  "exp": 1638363600, // 1 hour expiry
  "type": "access",
  "userId": 123,
  "modules": [1, 2, 3]
}

// Refresh Token
{
  "sub": "user@example.com",
  "iat": 1638360000,
  "exp": 1640952000, // 30 days expiry
  "type": "refresh",
  "userId": 123
}
```

**Token Security:**
- Tokens stored securely (not in localStorage for sensitive data)
- Short-lived access tokens (15-60 minutes)
- Longer-lived refresh tokens (7-30 days)
- Tokens transmitted only over HTTPS
- Token rotation on refresh
- Token revocation on logout

### Password Security

**Backend Requirements** (enforced by backend API):
- Minimum 8 characters
- Complexity requirements (uppercase, lowercase, numbers, symbols)
- Password history (prevent reuse)
- Hashing with bcrypt or Argon2
- Salting before hashing
- Rate limiting on login attempts

**Frontend Best Practices:**
```typescript
// Never log passwords
console.log('Login attempt for:', username); // ✅ Good
console.log('Password:', password); // ❌ Never do this

// Clear password from memory after use
let password = getUserInput();
await login(username, password);
password = null; // Clear variable

// Don't store passwords
localStorage.setItem('token', token); // ✅ Good
localStorage.setItem('password', password); // ❌ Never do this
```

### Multi-Factor Authentication (MFA)

**Support for MFA** (if implemented by backend):
- TOTP (Time-based One-Time Password)
- SMS codes
- Email codes
- Backup codes

**Implementation:**
```typescript
const loginWithMFA = async (username: string, password: string, mfaCode: string) => {
  const response = await axios.post('/auth/login', {
    username,
    password,
    mfaCode
  });
  return response.data;
};
```

### Session Management

**Session Security:**
- Absolute timeout (e.g., 24 hours)
- Idle timeout (e.g., 30 minutes)
- Concurrent session limits
- Secure session storage
- Session invalidation on logout

**Implementation:**
```typescript
// Track last activity
let lastActivity = Date.now();

// Update on user interaction
const updateActivity = () => {
  lastActivity = Date.now();
};

// Check for idle timeout
const checkIdleTimeout = () => {
  const idleTime = Date.now() - lastActivity;
  const maxIdle = 30 * 60 * 1000; // 30 minutes
  
  if (idleTime > maxIdle) {
    logout();
    showMessage('Session expired due to inactivity');
  }
};

// Check periodically
setInterval(checkIdleTimeout, 60000);
```

## Data Protection

### Sensitive Data Handling

**Classification:**
- **Public:** Non-sensitive data
- **Internal:** Internal use only
- **Confidential:** Sensitive business data
- **Restricted:** Highly sensitive (PII, credentials)

**Protection Measures:**

```typescript
// ❌ Bad - Exposing sensitive data
console.log('User data:', { 
  name: user.name,
  ssn: user.ssn, // Never log PII
  password: user.password // Never log passwords
});

// ✅ Good - Safe logging
console.log('User loaded:', {
  id: user.id,
  name: user.name
});
```

### Data at Rest

**Storage Security:**
- Sensitive data encrypted in backend database
- No sensitive data in browser localStorage
- Session tokens in secure httpOnly cookies (when possible)
- Temporary data cleared on logout

```typescript
// ❌ Bad
localStorage.setItem('creditCard', cardNumber);
localStorage.setItem('ssn', ssn);

// ✅ Good
// Store only non-sensitive data
localStorage.setItem('theme', 'dark');
localStorage.setItem('language', 'en');
```

### Data in Transit

**HTTPS Enforcement:**
- All API calls over HTTPS
- HSTS headers enabled
- No mixed content (HTTP resources on HTTPS page)

```typescript
// ✅ Ensure HTTPS
if (window.location.protocol !== 'https:' && 
    process.env.NODE_ENV === 'production') {
  window.location.href = 'https:' + window.location.href.substring(window.location.protocol.length);
}
```

### Data Sanitization

**Input Validation:**
```typescript
// Validate and sanitize user input
const sanitizeInput = (input: string): string => {
  // Remove potential XSS vectors
  return input
    .replace(/<script[^>]*>.*?<\/script>/gi, '')
    .replace(/<[^>]+>/g, '')
    .trim();
};

// Validate email
const isValidEmail = (email: string): boolean => {
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return emailRegex.test(email);
};
```

**Output Encoding:**
```typescript
// React automatically escapes JSX content
// But be careful with dangerouslySetInnerHTML

// ❌ Dangerous
<div dangerouslySetInnerHTML={{ __html: userContent }} />

// ✅ Safe alternative
import DOMPurify from 'dompurify';
<div dangerouslySetInnerHTML={{ 
  __html: DOMPurify.sanitize(userContent) 
}} />
```

## API Security

### Request Security

**CORS Configuration:**
```typescript
// Backend should configure CORS properly
// Allow only trusted origins
Access-Control-Allow-Origin: https://hexmate.example.com
Access-Control-Allow-Methods: GET, POST, PUT, DELETE
Access-Control-Allow-Headers: Authorization, Content-Type
Access-Control-Allow-Credentials: true
```

**Request Authentication:**
```typescript
// Always include authentication token
const apiClient = axios.create({
  baseURL: process.env.REACT_APP_BASE_API,
  headers: {
    'Content-Type': 'application/json',
  },
});

apiClient.interceptors.request.use((config) => {
  const token = getAccessToken();
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});
```

### Rate Limiting

**Client-Side Rate Limiting:**
```typescript
// Implement basic rate limiting
class RateLimiter {
  private requests: number[] = [];
  private limit: number;
  private window: number;

  constructor(limit: number, windowMs: number) {
    this.limit = limit;
    this.window = windowMs;
  }

  async throttle(): Promise<void> {
    const now = Date.now();
    this.requests = this.requests.filter(time => now - time < this.window);
    
    if (this.requests.length >= this.limit) {
      const oldestRequest = this.requests[0];
      const waitTime = this.window - (now - oldestRequest);
      await new Promise(resolve => setTimeout(resolve, waitTime));
    }
    
    this.requests.push(now);
  }
}

const apiLimiter = new RateLimiter(100, 60000); // 100 requests per minute

const makeApiCall = async (url: string) => {
  await apiLimiter.throttle();
  return axios.get(url);
};
```

### API Error Handling

```typescript
// Don't expose sensitive error details
apiClient.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response) {
      // Log full error for debugging (server-side)
      console.error('API Error:', error.response);
      
      // Show user-friendly message
      const userMessage = error.response.status === 403
        ? 'Access denied'
        : error.response.status === 404
        ? 'Resource not found'
        : 'An error occurred';
      
      showNotification(userMessage);
    }
    return Promise.reject(error);
  }
);
```

## Frontend Security

### XSS Prevention

**React Built-in Protection:**
```typescript
// ✅ React automatically escapes
const username = "<script>alert('xss')</script>";
<div>{username}</div> // Renders as text, not executed

// ❌ Bypass protection - avoid unless absolutely necessary
<div dangerouslySetInnerHTML={{ __html: userContent }} />
```

**URL Parameters:**
```typescript
// Sanitize URL parameters
const params = new URLSearchParams(window.location.search);
const searchQuery = params.get('q');

// Validate before use
if (searchQuery && /^[a-zA-Z0-9\s]+$/.test(searchQuery)) {
  performSearch(searchQuery);
}
```

### CSRF Protection

**Token-Based Protection:**
```typescript
// Backend should provide CSRF token
// Include in forms and AJAX requests

const form = document.querySelector('form');
const csrfToken = document.querySelector('meta[name="csrf-token"]')?.content;

if (csrfToken) {
  form.addEventListener('submit', (e) => {
    const input = document.createElement('input');
    input.type = 'hidden';
    input.name = 'csrf_token';
    input.value = csrfToken;
    form.appendChild(input);
  });
}
```

### Content Security Policy

**CSP Headers:**
```html
<!-- Set via backend or meta tag -->
<meta http-equiv="Content-Security-Policy" 
      content="
        default-src 'self';
        script-src 'self' 'unsafe-inline' 'unsafe-eval';
        style-src 'self' 'unsafe-inline';
        img-src 'self' data: https:;
        font-src 'self' data:;
        connect-src 'self' https://api.hexmate.example.com;
      ">
```

### Clickjacking Prevention

```typescript
// Backend should set X-Frame-Options header
X-Frame-Options: DENY
// or
X-Frame-Options: SAMEORIGIN

// Client-side check
if (window.top !== window.self) {
  // Page is in an iframe
  window.top.location = window.self.location;
}
```

## Deployment Security

### HTTPS Enforcement

**Nginx Configuration:**
```nginx
# Redirect HTTP to HTTPS
server {
    listen 80;
    server_name hexmate.example.com;
    return 301 https://$server_name$request_uri;
}

# HTTPS server
server {
    listen 443 ssl http2;
    server_name hexmate.example.com;
    
    ssl_certificate /path/to/cert.pem;
    ssl_certificate_key /path/to/key.pem;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;
    
    # HSTS
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
}
```

### Security Headers

```nginx
# Security headers
add_header X-Frame-Options "SAMEORIGIN" always;
add_header X-Content-Type-Options "nosniff" always;
add_header X-XSS-Protection "1; mode=block" always;
add_header Referrer-Policy "no-referrer-when-downgrade" always;
add_header Permissions-Policy "geolocation=(), microphone=(), camera=()" always;
```

### Environment Variables

```bash
# ❌ Never commit secrets to repository
REACT_APP_API_KEY=abc123secret

# ✅ Use environment-specific files
.env.local        # Local development (gitignored)
.env.production   # Production (never committed)

# ✅ Use secure secret management
# - AWS Secrets Manager
# - Azure Key Vault
# - HashiCorp Vault
```

## Security Best Practices

### Code Security

1. **Dependency Security**
   ```bash
   # Regular security audits
   npm audit
   npm audit fix
   
   # Check for known vulnerabilities
   npm install -g snyk
   snyk test
   ```

2. **Code Review**
   - Review all code changes
   - Security-focused reviews for sensitive code
   - Automated security scanning
   - Penetration testing

3. **Secrets Management**
   - Never hardcode secrets
   - Use environment variables
   - Rotate secrets regularly
   - Use secret management services

### User Security

1. **Account Security**
   - Strong password enforcement
   - Account lockout after failed attempts
   - Password change on first login
   - Regular password expiry
   - MFA enablement

2. **Access Control**
   - Role-based access control
   - Principle of least privilege
   - Regular permission reviews
   - Audit logs for access

3. **User Education**
   - Security awareness training
   - Phishing prevention
   - Password best practices
   - Incident reporting procedures

## Compliance

### Data Privacy

**GDPR Compliance:**
- Data minimization
- Purpose limitation
- Storage limitation
- Right to access
- Right to erasure
- Data portability
- Consent management

**Implementation:**
```typescript
// Provide data export
const exportUserData = async (userId: number) => {
  const userData = await getUserData(userId);
  // Export in portable format (JSON, CSV)
  return JSON.stringify(userData);
};

// Implement data deletion
const deleteUserData = async (userId: number) => {
  // Anonymize or delete user data
  await anonymizeUser(userId);
  await deleteUserRecords(userId);
};
```

### Audit Logging

**Log Security Events:**
```typescript
const auditLog = {
  timestamp: new Date().toISOString(),
  userId: user.id,
  action: 'LOGIN_SUCCESS',
  ipAddress: request.ip,
  userAgent: request.headers['user-agent'],
  resource: null,
  result: 'SUCCESS'
};

// Log to backend
await logAuditEvent(auditLog);
```

**Events to Log:**
- Authentication (login, logout, failed attempts)
- Authorization (access granted/denied)
- Data access (view, create, update, delete)
- Configuration changes
- Security events (password change, permission change)

## Security Checklist

### Development

- [ ] Input validation on all user inputs
- [ ] Output encoding for dynamic content
- [ ] Parameterized queries (backend)
- [ ] Error handling doesn't expose sensitive info
- [ ] Secrets not hardcoded
- [ ] Dependencies up to date
- [ ] Security linting enabled

### Deployment

- [ ] HTTPS enforced
- [ ] Security headers configured
- [ ] CORS properly configured
- [ ] Rate limiting enabled
- [ ] Logging and monitoring active
- [ ] Backup strategy in place
- [ ] Incident response plan ready

### Ongoing

- [ ] Regular security audits
- [ ] Dependency vulnerability scanning
- [ ] Penetration testing
- [ ] Security training for team
- [ ] Incident response drills
- [ ] Regular backup testing
- [ ] Access review and cleanup

## Resources

- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/)
- [React Security Best Practices](https://reactjs.org/docs/dom-elements.html#dangerouslysetinnerhtml)
- [Web Security Academy](https://portswigger.net/web-security)

## Contact

For security concerns or questions:
- GitHub Issues: For non-sensitive security discussions
- Direct Contact: Reach out to repository maintainers privately for sensitive security issues
