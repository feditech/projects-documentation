# Troubleshooting Guide

## Table of Contents

- [Common Issues](#common-issues)
- [Installation Problems](#installation-problems)
- [Login & Authentication Issues](#login--authentication-issues)
- [Performance Issues](#performance-issues)
- [UI/Display Issues](#uidisplay-issues)
- [API & Network Issues](#api--network-issues)
- [Build & Deployment Issues](#build--deployment-issues)
- [Browser-Specific Issues](#browser-specific-issues)
- [Error Messages](#error-messages)
- [Getting Help](#getting-help)

## Common Issues

### Application Won't Start

**Symptoms**: Error when running `npm start`

**Solutions**:

1. **Check Node.js version**:
```bash
node --version
# Should be v14 or higher
```

2. **Clear node_modules and reinstall**:
```bash
rm -rf node_modules package-lock.json
npm install
```

3. **Check for port conflicts**:
```bash
# Port 3000 might be in use
lsof -ti:3000  # macOS/Linux
netstat -ano | findstr :3000  # Windows

# Kill the process or use different port
PORT=3001 npm start
```

4. **Check for syntax errors**:
```bash
npm run build
# Check console for errors
```

### White Screen After Login

**Symptoms**: Blank white page after successful login

**Solutions**:

1. **Check browser console**:
   - Open DevTools (F12)
   - Look for JavaScript errors
   - Look for failed network requests

2. **Clear browser cache**:
   - Clear cache and cookies
   - Hard refresh (Ctrl+Shift+R or Cmd+Shift+R)

3. **Check API connectivity**:
```javascript
// Test API endpoint
fetch(process.env.REACT_APP_API_BASE_URL + '/health')
  .then(response => console.log('API Status:', response.status))
  .catch(error => console.error('API Error:', error));
```

4. **Verify environment variables**:
   - Check `.env` file exists
   - Verify REACT_APP_API_BASE_URL is set
   - Restart development server after changing .env

### Data Not Loading

**Symptoms**: Tables or lists show no data or loading spinner never stops

**Solutions**:

1. **Check network requests**:
   - Open DevTools → Network tab
   - Filter by XHR/Fetch
   - Look for failed requests (red)
   - Check response status codes

2. **Verify API endpoint**:
   - Check endpoint URL is correct
   - Verify endpoint exists on backend
   - Test endpoint with Postman/curl

3. **Check authentication token**:
   - Token might be expired
   - Log out and log back in
   - Check Redux store for token

4. **Check browser console for errors**:
   - Look for CORS errors
   - Look for permission errors
   - Check for network errors

## Installation Problems

### npm install Fails

**Error**: `npm ERR! peer dependency conflicts`

**Solution**:
```bash
npm install --legacy-peer-deps
```

**Error**: `EACCES: permission denied`

**Solution**:
```bash
# Don't use sudo! Fix npm permissions instead
# Option 1: Use a Node version manager (recommended)
# Install nvm and use it to install Node

# Option 2: Change npm's default directory
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'
export PATH=~/.npm-global/bin:$PATH
```

### Dependency Version Conflicts

**Error**: Incompatible package versions

**Solutions**:

1. **Update package.json**:
```bash
npm update
```

2. **Use specific versions**:
```bash
npm install package-name@specific-version
```

3. **Check for breaking changes**:
   - Review package changelogs
   - Update code if needed

## Login & Authentication Issues

### Can't Log In

**Symptoms**: Login fails with incorrect credentials or error

**Solutions**:

1. **Verify credentials**:
   - Double-check email and password
   - Check for typos
   - Ensure Caps Lock is off

2. **Reset password**:
   - Use "Forgot Password" feature
   - Check email for reset link
   - Check spam folder

3. **Check API status**:
   - Verify backend is running
   - Check API URL in .env
   - Test login endpoint directly

4. **Clear stored data**:
```javascript
// Clear localStorage
localStorage.clear();
sessionStorage.clear();
// Refresh page
```

### Session Expires Too Quickly

**Symptoms**: Logged out frequently

**Solutions**:

1. **Check token expiration settings** (backend)
2. **Implement token refresh**:
```javascript
// Auto-refresh token before expiry
const refreshToken = async () => {
  const response = await Api.post('/auth/refresh');
  // Update token in Redux
};
```

3. **Adjust inactivity timeout**

### Token Not Being Sent

**Symptoms**: API returns 401 Unauthorized despite being logged in

**Solutions**:

1. **Check Axios interceptor**:
```javascript
// Verify interceptor is configured
Api.interceptors.request.use(
  config => {
    const token = getToken();
    if (token) {
      config.headers.Authorization = `Bearer ${token}`;
    }
    return config;
  }
);
```

2. **Check token storage**:
```javascript
// Verify token is in Redux store
const token = store.getState().activeAccount.token;
console.log('Token:', token ? 'Present' : 'Missing');
```

## Performance Issues

### Slow Page Load

**Symptoms**: Pages take long time to load

**Solutions**:

1. **Check network speed**:
   - Run speed test
   - Check for network congestion
   - Try different network

2. **Optimize images**:
   - Compress images before upload
   - Use appropriate image formats
   - Implement lazy loading

3. **Reduce bundle size**:
```bash
# Analyze bundle
npm run build
npm install -g source-map-explorer
source-map-explorer 'build/static/js/*.js'
```

4. **Enable code splitting**:
```javascript
// Use React.lazy for route-based splitting
const DoctorProfiles = lazy(() => import('./screens/doctors/Profiles'));
```

### High Memory Usage

**Symptoms**: Browser becomes slow or crashes

**Solutions**:

1. **Check for memory leaks**:
   - Look for unmounted components still updating state
   - Cancel pending requests on unmount
   - Clean up event listeners

```javascript
useEffect(() => {
  const fetchData = async () => {
    const response = await Api.get('/endpoint');
    // Process response
  };
  
  fetchData();
  
  // Cleanup
  return () => {
    // Cancel requests, clear timers, etc.
  };
}, []);
```

2. **Limit data rendered**:
   - Use pagination
   - Implement virtual scrolling for large lists
   - Limit table page size

3. **Use React.memo**:
```javascript
const ExpensiveComponent = React.memo(({ data }) => {
  // Component logic
});
```

## UI/Display Issues

### Layout Broken

**Symptoms**: Components overlapping or misaligned

**Solutions**:

1. **Clear browser cache**
2. **Check CSS conflicts**
3. **Verify Material-UI version compatibility**
4. **Check for missing CSS imports**

### Icons Not Displaying

**Symptoms**: Icon placeholders or boxes instead of icons

**Solutions**:

1. **Check icon imports**:
```javascript
// Verify icon is imported
import { Add, Edit, Delete } from '@mui/icons-material';
```

2. **Check Material Icons font**:
```html
<!-- Verify in index.html -->
<link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons" />
```

3. **Clear browser cache**

### Responsive Issues on Mobile

**Symptoms**: Layout doesn't adapt to mobile screens

**Solutions**:

1. **Check viewport meta tag**:
```html
<meta name="viewport" content="width=device-width, initial-scale=1" />
```

2. **Test with browser DevTools**:
   - Open DevTools
   - Toggle device toolbar
   - Test different screen sizes

3. **Check media queries**:
```css
@media (max-width: 768px) {
  /* Mobile styles */
}
```

## API & Network Issues

### CORS Errors

**Error**: `Access-Control-Allow-Origin header`

**Solutions**:

1. **Configure backend CORS** (backend team):
```javascript
// Backend must allow your domain
cors({
  origin: 'http://localhost:3000',
  credentials: true
})
```

2. **Check API URL**:
   - Ensure using correct protocol (http/https)
   - Verify domain is correct

3. **Development workaround**:
```javascript
// Use proxy in package.json
"proxy": "http://localhost:5000"
```

### Network Timeout

**Error**: Request timeout

**Solutions**:

1. **Increase timeout**:
```javascript
const Api = axios.create({
  baseURL: process.env.REACT_APP_API_BASE_URL,
  timeout: 30000, // 30 seconds
});
```

2. **Check backend performance**
3. **Check network connectivity**

### 500 Internal Server Error

**Error**: API returns 500 status

**Solutions**:

1. **Check backend logs** (backend team)
2. **Verify request payload**:
```javascript
// Log request before sending
console.log('Request:', data);
```

3. **Check for required fields**
4. **Verify data types match API expectations**

## Build & Deployment Issues

### Build Fails

**Error**: `npm run build` fails

**Solutions**:

1. **Check for errors**:
```bash
npm run build 2>&1 | tee build-log.txt
# Review build-log.txt
```

2. **Check for unused imports**:
```bash
# Run ESLint
npm run lint
```

3. **Check for TypeScript errors** (if using TypeScript)

4. **Clear cache and rebuild**:
```bash
rm -rf build node_modules package-lock.json
npm install
npm run build
```

### Environment Variables Not Working in Production

**Symptoms**: API calls fail in production

**Solutions**:

1. **Verify REACT_APP_ prefix**:
```javascript
// ✅ Correct
REACT_APP_API_BASE_URL=https://api.example.com

// ❌ Wrong
API_BASE_URL=https://api.example.com
```

2. **Rebuild after changing .env**:
```bash
npm run build
```

3. **Check hosting platform**:
   - Verify environment variables are set
   - Use platform-specific configuration

### Production Build Too Large

**Symptoms**: Slow initial load

**Solutions**:

1. **Analyze bundle**:
```bash
npm run build
npm install -g source-map-explorer
source-map-explorer 'build/static/js/*.js'
```

2. **Remove unused dependencies**:
```bash
npm uninstall unused-package
```

3. **Code splitting**:
```javascript
const LazyComponent = lazy(() => import('./LazyComponent'));
```

4. **Optimize images**:
   - Compress images
   - Use WebP format
   - Lazy load images

## Browser-Specific Issues

### Works in Chrome but not Safari

**Solutions**:

1. **Check for browser-specific CSS**
2. **Test JavaScript features**:
   - Use polyfills if needed
   - Check babel configuration

3. **Check browser console** for errors

### Internet Explorer Issues

**Note**: Modern browsers (Chrome, Firefox, Safari, Edge) are recommended

**Solutions**:

1. **Add polyfills**:
```bash
npm install react-app-polyfill
```

```javascript
// Add to index.js
import 'react-app-polyfill/ie11';
import 'react-app-polyfill/stable';
```

2. **Update browserslist** in package.json

## Error Messages

### "Cannot read property 'X' of undefined"

**Cause**: Accessing property of null/undefined object

**Solutions**:

1. **Add null checks**:
```javascript
// ❌ Risky
const name = user.profile.name;

// ✅ Safe
const name = user?.profile?.name || 'Unknown';
```

2. **Provide default values**:
```javascript
const { data = [] } = response;
```

### "Maximum update depth exceeded"

**Cause**: Infinite loop in useEffect or setState

**Solutions**:

1. **Check useEffect dependencies**:
```javascript
// ❌ Wrong - causes infinite loop
useEffect(() => {
  setCount(count + 1);
}); // Missing dependency array

// ✅ Correct
useEffect(() => {
  setCount(count + 1);
}, []); // Empty array - runs once
```

2. **Avoid setting state in render**:
```javascript
// ❌ Wrong
const MyComponent = () => {
  setState(newValue); // Causes infinite loop
  return <div>...</div>;
};

// ✅ Correct
const MyComponent = () => {
  useEffect(() => {
    setState(newValue);
  }, []);
  return <div>...</div>;
};
```

### "Objects are not valid as a React child"

**Cause**: Trying to render object instead of string/number

**Solutions**:

```javascript
// ❌ Wrong
return <div>{user}</div>; // user is an object

// ✅ Correct
return <div>{user.name}</div>; // Render specific property
return <div>{JSON.stringify(user)}</div>; // Or stringify for debugging
```

## Getting Help

### Self-Help Resources

1. **Check documentation**: Review relevant documentation files
2. **Search issues**: Check GitHub issues for similar problems
3. **Browser console**: Check for error messages
4. **Network tab**: Inspect API requests/responses
5. **Redux DevTools**: Check application state

### Gathering Information

Before asking for help, collect:

1. **Error messages**: Full text and stack trace
2. **Steps to reproduce**: Detailed steps
3. **Environment**:
   - Browser and version
   - Operating system
   - Node.js version
   - Package versions
4. **Screenshots**: Visual issues
5. **Network logs**: Failed API requests
6. **Console logs**: JavaScript errors

### Reporting Bugs

Include in bug report:

```markdown
## Bug Description
Brief description of the issue

## Steps to Reproduce
1. Go to...
2. Click on...
3. See error...

## Expected Behavior
What should happen

## Actual Behavior
What actually happens

## Environment
- Browser: Chrome 98.0
- OS: macOS 12.1
- Node: v16.13.0
- App Version: 0.1.0

## Screenshots
[Attach screenshots]

## Console Errors
[Paste error messages]

## Additional Context
Any other relevant information
```

### Contact Support

- **Email**: support@doclink.com
- **GitHub Issues**: Create an issue in the repository
- **Internal Chat**: Use team communication channels
- **Documentation**: Refer to other documentation files

### Emergency Contacts

For critical production issues:
- **On-call Engineer**: [Contact Info]
- **Team Lead**: [Contact Info]
- **DevOps**: [Contact Info]

---

**Remember**: Most issues can be resolved by:
1. Checking the browser console
2. Clearing cache and refreshing
3. Verifying environment variables
4. Restarting the development server

If you've tried these and still have issues, don't hesitate to ask for help!
