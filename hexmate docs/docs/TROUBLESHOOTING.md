# Troubleshooting Guide

This guide helps you diagnose and resolve common issues in HexMate.

## Table of Contents

- [Installation Issues](#installation-issues)
- [Configuration Issues](#configuration-issues)
- [Runtime Issues](#runtime-issues)
- [Authentication Issues](#authentication-issues)
- [Module-Specific Issues](#module-specific-issues)
- [Performance Issues](#performance-issues)
- [Build and Deployment Issues](#build-and-deployment-issues)
- [Browser Issues](#browser-issues)
- [Getting Help](#getting-help)

## Installation Issues

### npm install fails

**Symptom:** Installation errors or failures during `npm install`

**Possible Causes:**
- Insufficient permissions
- Network issues
- Incompatible Node.js version
- Corrupted npm cache

**Solutions:**

1. **Check Node.js version:**
   ```bash
   node --version  # Should be 16.x or higher
   npm --version   # Should be 7.x or higher
   ```

2. **Clear npm cache:**
   ```bash
   npm cache clean --force
   rm -rf node_modules package-lock.json
   npm install
   ```

3. **Fix permissions (Unix/Linux/macOS):**
   ```bash
   sudo chown -R $USER:$(id -gn $USER) ~/.npm
   sudo chown -R $USER:$(id -gn $USER) ~/.config
   ```

4. **Use different registry (if corporate firewall):**
   ```bash
   npm config set registry https://registry.npmjs.org/
   # Or use your corporate registry
   npm install
   ```

5. **Install with legacy peer deps:**
   ```bash
   npm install --legacy-peer-deps
   ```

### DWT resources not copying

**Symptom:** `dwt-resources` folder missing after install

**Solution:**
```bash
# Manually copy DWT resources
npx ncp node_modules/dwt/dist public/dwt-resources
```

### Module not found errors

**Symptom:** Import errors like "Cannot find module 'react'"

**Solutions:**

1. **Reinstall dependencies:**
   ```bash
   rm -rf node_modules package-lock.json
   npm install
   ```

2. **Check TypeScript configuration:**
   ```bash
   # Verify tsconfig.json includes src directory
   cat tsconfig.json | grep include
   ```

3. **Restart development server:**
   ```bash
   # Stop server (Ctrl+C)
   npm start
   ```

## Configuration Issues

### Environment variables not working

**Symptom:** API calls fail or configuration not applied

**Solutions:**

1. **Verify .env file exists:**
   ```bash
   ls -la | grep .env
   ```

2. **Check variable naming:**
   - Must start with `REACT_APP_`
   - Example: `REACT_APP_BASE_API=https://api.example.com/api/`

3. **Restart development server:**
   ```bash
   # Changes to .env require server restart
   # Stop (Ctrl+C) and restart
   npm start
   ```

4. **Verify variable is set:**
   ```typescript
   console.log('API URL:', process.env.REACT_APP_BASE_API);
   ```

5. **Check for spaces:**
   ```bash
   # ❌ Wrong - has spaces
   REACT_APP_BASE_API = https://api.example.com/api/
   
   # ✅ Correct - no spaces
   REACT_APP_BASE_API=https://api.example.com/api/
   ```

### config.json not loading

**Symptom:** Modules not appearing, blank page, or configuration errors

**Solutions:**

1. **Verify file exists:**
   ```bash
   cat public/config.json
   ```

2. **Validate JSON syntax:**
   ```bash
   # Use online JSON validator or
   cat public/config.json | python -m json.tool
   ```

3. **Check file permissions:**
   ```bash
   chmod 644 public/config.json
   ```

4. **Hard refresh browser:**
   - Chrome/Firefox: `Ctrl+Shift+R` (Windows/Linux) or `Cmd+Shift+R` (Mac)
   - Clear browser cache

5. **Verify correct format:**
   ```json
   {
     "modules": [
       {"id": 1, "name": "DMS", "link": "/dms/documents"}
     ]
   }
   ```

### Module not appearing

**Symptom:** Module listed in config.json but not visible in UI

**Solutions:**

1. **Check user has module access:**
   - User must have module ID in their `modules` field
   - Admin users see all modules
   - Contact administrator to grant access

2. **Verify config.json:**
   ```json
   {
     "modules": [
       {"id": 1, "name": "DMS", "link": "/dms/documents"},
       {"id": 2, "name": "CTS", "link": "/cts/dashboard"},
       {"id": 3, "name": "VMS", "link": "/vms/dashboard"}
     ]
   }
   ```

3. **Check browser console:**
   ```
   F12 → Console tab → Look for errors
   ```

## Runtime Issues

### Blank page on load

**Symptom:** Application shows blank page

**Solutions:**

1. **Check browser console:**
   ```
   Press F12 → Console tab
   Look for JavaScript errors
   ```

2. **Common errors and fixes:**

   **"Cannot read property of undefined":**
   - Data structure mismatch
   - API response format changed
   - Check API endpoint

   **"Failed to fetch":**
   - API server not running
   - Wrong API URL in .env
   - CORS issue

   **"Syntax error":**
   - Build issue
   - Clear cache and rebuild

3. **Clear browser data:**
   ```
   Chrome: Settings → Privacy → Clear browsing data
   Select: Cached images and files, Cookies
   ```

4. **Try incognito/private mode:**
   - Rules out extension conflicts
   - Tests with clean state

5. **Check PUBLIC_URL:**
   ```bash
   # If deployed to subdirectory
   PUBLIC_URL=/hexmate npm start
   ```

### Page not found (404)

**Symptom:** Navigating to routes shows 404 error

**Solutions:**

1. **Development mode:**
   - Should work automatically with webpack dev server
   - Restart development server

2. **Production deployment:**
   - Configure web server for SPA routing
   - See [Deployment Guide](DEPLOYMENT.md) for server configuration

3. **Verify route exists:**
   ```typescript
   // Check App.tsx for route definition
   <Route path="/your-route" element={<YourComponent />} />
   ```

### Infinite loading state

**Symptom:** Loading spinner never stops

**Solutions:**

1. **Check API connectivity:**
   ```bash
   # Test API endpoint
   curl https://api.example.com/api/health
   ```

2. **Check browser console:**
   - Network tab for failed requests
   - Console tab for JavaScript errors

3. **Verify authentication:**
   - Token might be expired
   - Try logging out and back in

4. **Check for JavaScript errors:**
   - Unhandled promise rejections
   - Missing error handling

## Authentication Issues

### Cannot log in

**Symptom:** Login fails with error or no response

**Solutions:**

1. **Verify credentials:**
   - Check username/email
   - Check password (case-sensitive)
   - Check caps lock

2. **Check API endpoint:**
   ```bash
   # Test login endpoint
   curl -X POST https://api.example.com/api/auth/login \
     -H "Content-Type: application/json" \
     -d '{"username":"test","password":"test"}'
   ```

3. **Check CORS:**
   - Backend must allow frontend origin
   - Check browser console for CORS errors
   - Verify backend CORS configuration

4. **Check account status:**
   - Account might be locked
   - Account might be inactive
   - Contact administrator

5. **Backend server issues:**
   - Verify backend is running
   - Check backend logs
   - Database connection issues

### Session expires immediately

**Symptom:** Logged out right after login

**Solutions:**

1. **Check token expiry:**
   - Token might have very short expiry
   - Check backend configuration

2. **Check system time:**
   - Ensure system clock is correct
   - Time sync with NTP server

3. **Check browser storage:**
   ```javascript
   // Open console and check
   console.log(localStorage.getItem('accessToken'));
   console.log(localStorage.getItem('refreshToken'));
   ```

4. **Clear storage and retry:**
   ```javascript
   localStorage.clear();
   sessionStorage.clear();
   // Then log in again
   ```

### Unauthorized errors on API calls

**Symptom:** API calls fail with 401 Unauthorized

**Solutions:**

1. **Check token presence:**
   ```javascript
   // In browser console
   console.log(localStorage.getItem('accessToken'));
   ```

2. **Check token format:**
   ```javascript
   // Should be: Bearer {token}
   console.log('Auth header:', axios.defaults.headers.common['Authorization']);
   ```

3. **Token expired:**
   - Log out and log back in
   - Check token refresh mechanism

4. **Wrong API endpoint:**
   - Verify REACT_APP_BASE_API is correct
   - Check for trailing slash

## Module-Specific Issues

### DMS: Cannot upload documents

**Symptom:** Document upload fails or hangs

**Solutions:**

1. **Check file size:**
   - Verify file is within size limits
   - Check backend upload limits
   - Check web server limits (nginx/apache)

2. **Check permissions:**
   - User must have upload permission
   - Check folder permissions
   - Verify user is not read-only

3. **Check file type:**
   - Verify file type is allowed
   - Check backend configuration
   - Try different file format

4. **Network timeout:**
   - Large files may timeout
   - Increase timeout settings
   - Use chunked upload if available

### DMS: Document scanner not working

**Symptom:** Scanner integration fails

**Solutions:**

1. **Check DWT resources:**
   ```bash
   ls -la public/dwt-resources
   ```

2. **Copy resources if missing:**
   ```bash
   npx ncp node_modules/dwt/dist public/dwt-resources
   ```

3. **Check scanner connection:**
   - Scanner must be TWAIN-compatible
   - Scanner must be connected and on
   - Install scanner drivers

4. **Browser compatibility:**
   - Use Chrome or Firefox
   - Enable required browser permissions
   - Check for plugin blockers

### CTS: Routing not working

**Symptom:** Correspondence not routing to groups

**Solutions:**

1. **Check routing rules:**
   - Navigate to Routing Groups settings
   - Verify rules are configured
   - Check rule conditions match

2. **Check group members:**
   - Routing group must have members
   - Members must be active users
   - Check delegation status

3. **Check workflow:**
   - Verify workflow is active
   - Check workflow configuration
   - Review workflow logs

### VMS: QR code not generating

**Symptom:** Appointment confirmation without QR code

**Solutions:**

1. **Check appointment status:**
   - Must be approved
   - Must have valid date
   - Check for errors in details

2. **Check email template:**
   - Template must include QR code
   - Verify template configuration
   - Test email sending

3. **Check browser:**
   - Clear cache
   - Try different browser
   - Disable ad blockers

## Performance Issues

### Slow page load

**Symptom:** Pages take long time to load

**Solutions:**

1. **Check network:**
   ```bash
   # Test API response time
   curl -w "@curl-format.txt" -o /dev/null -s https://api.example.com/api/
   ```

2. **Check bundle size:**
   ```bash
   npm run build
   # Check build/static/js/*.js file sizes
   ```

3. **Optimize images:**
   - Compress large images
   - Use appropriate formats
   - Implement lazy loading

4. **Clear browser cache:**
   - Hard refresh (Ctrl+Shift+R)
   - Clear all cached data

5. **Check API performance:**
   - Review backend logs
   - Check database queries
   - Optimize API endpoints

### Memory leaks

**Symptom:** Browser becomes slow over time

**Solutions:**

1. **Check for memory leaks:**
   ```
   Chrome DevTools → Memory tab
   Take heap snapshot
   Perform actions
   Take another snapshot
   Compare
   ```

2. **Common causes:**
   - Event listeners not cleaned up
   - Timers not cleared
   - Large arrays/objects in state

3. **Fix examples:**
   ```typescript
   // ✅ Clean up effect
   useEffect(() => {
     const interval = setInterval(() => {}, 1000);
     return () => clearInterval(interval);
   }, []);

   // ✅ Clean up event listener
   useEffect(() => {
     const handleScroll = () => {};
     window.addEventListener('scroll', handleScroll);
     return () => window.removeEventListener('scroll', handleScroll);
   }, []);
   ```

### High CPU usage

**Symptom:** Browser tab uses excessive CPU

**Solutions:**

1. **Check for infinite loops:**
   - Review recent code changes
   - Check useEffect dependencies
   - Look for recursive calls

2. **Optimize rendering:**
   ```typescript
   // Use React.memo for expensive components
   const ExpensiveComponent = React.memo(({ data }) => {
     // Component code
   });

   // Use useMemo for expensive computations
   const expensiveValue = useMemo(() => {
     return computeExpensiveValue(data);
   }, [data]);

   // Use useCallback for functions
   const handleClick = useCallback(() => {
     // Handler code
   }, [dependencies]);
   ```

3. **Reduce re-renders:**
   - Check state updates
   - Avoid unnecessary prop changes
   - Use proper key props in lists

## Build and Deployment Issues

### Build fails

**Symptom:** `npm run build` fails with errors

**Solutions:**

1. **Check TypeScript errors:**
   ```bash
   npx tsc --noEmit
   ```

2. **Check for linting errors:**
   ```bash
   npx eslint src/
   ```

3. **Clear cache and rebuild:**
   ```bash
   rm -rf node_modules package-lock.json build
   npm install
   npm run build
   ```

4. **Check Node.js memory:**
   ```bash
   # Increase memory limit
   NODE_OPTIONS="--max-old-space-size=4096" npm run build
   ```

5. **Check for missing dependencies:**
   ```bash
   npm install
   npm run build
   ```

### Deployed app shows blank page

**Symptom:** Production deployment shows blank page

**Solutions:**

1. **Check PUBLIC_URL:**
   ```bash
   # If deployed to subdirectory
   PUBLIC_URL=/hexmate npm run build
   ```

2. **Check server configuration:**
   - Web server must serve index.html for all routes
   - See [Deployment Guide](DEPLOYMENT.md)

3. **Check console errors:**
   - Open browser console
   - Look for 404 errors
   - Check paths in errors

4. **Check file permissions:**
   ```bash
   # Make files readable
   chmod -R 755 build/
   ```

5. **Verify API URL:**
   - Check .env.production
   - Verify REACT_APP_BASE_API is correct

### Assets not loading

**Symptom:** 404 errors for CSS/JS/images

**Solutions:**

1. **Check PUBLIC_URL:**
   - Must match deployment path
   - Include leading slash, no trailing slash

2. **Check web server config:**
   - Static file serving enabled
   - Correct document root

3. **Check file paths:**
   - Use relative paths or PUBLIC_URL
   - Avoid hardcoded absolute paths

4. **Check MIME types:**
   - Web server must serve correct MIME types
   - Add to nginx/apache configuration if needed

## Browser Issues

### Not working in Internet Explorer

**Symptom:** Application doesn't work in IE

**Note:** HexMate does not support Internet Explorer. Use modern browsers:
- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

### Mobile responsive issues

**Symptom:** Layout broken on mobile devices

**Solutions:**

1. **Check viewport meta tag:**
   ```html
   <meta name="viewport" content="width=device-width, initial-scale=1" />
   ```

2. **Test in mobile view:**
   - Chrome DevTools → Toggle device toolbar
   - Test different screen sizes

3. **Check Material-UI breakpoints:**
   ```typescript
   // Use responsive props
   <Grid container spacing={2}>
     <Grid item xs={12} md={6}>
       {/* Content */}
     </Grid>
   </Grid>
   ```

### Browser extensions causing issues

**Symptom:** Application works in incognito but not normal mode

**Solutions:**

1. **Test in incognito/private mode:**
   - Chrome: Ctrl+Shift+N
   - Firefox: Ctrl+Shift+P

2. **Disable extensions:**
   - Disable ad blockers
   - Disable privacy extensions
   - Disable script blockers

3. **Common problematic extensions:**
   - Ad blockers (uBlock, AdBlock)
   - Privacy Badger
   - NoScript
   - HTTPS Everywhere

## Getting Help

### Before Asking for Help

1. **Check this guide** thoroughly
2. **Search existing issues** on GitHub
3. **Check browser console** for errors
4. **Try in different browser**
5. **Collect information:**
   - Operating system and version
   - Browser and version
   - Node.js and npm versions
   - Steps to reproduce
   - Error messages (full text)
   - Screenshots

### Where to Get Help

1. **Documentation:**
   - Read relevant docs in `/docs`
   - Check module user manuals (PDFs)

2. **GitHub Issues:**
   - Search: https://github.com/feditech/hexmate/issues
   - Create new issue if not found

3. **Create Good Issue:**
   ```markdown
   **Environment:**
   - OS: Windows 10
   - Browser: Chrome 96
   - Node: 16.13.0
   - npm: 8.1.0

   **Steps to Reproduce:**
   1. Login as regular user
   2. Navigate to /dms/documents
   3. Click "Upload" button
   4. Select PDF file
   5. Click "Submit"

   **Expected:**
   Document should upload successfully

   **Actual:**
   Error: "Upload failed" appears

   **Console Errors:**
   [Include any console errors]

   **Screenshots:**
   [Attach relevant screenshots]
   ```

4. **Emergency Issues:**
   - For security issues: See [Security Policy](SECURITY.md)
   - For production outages: Contact system administrator

### Diagnostic Information

Collect this information when reporting issues:

```bash
# System information
node --version
npm --version
git --version

# Package information
npm list --depth=0

# Browser information
# Open in browser console:
console.log(navigator.userAgent);

# Check environment
echo $REACT_APP_BASE_API
```

## Additional Resources

- [Installation Guide](INSTALLATION.md)
- [Configuration Guide](CONFIGURATION.md)
- [Development Guide](DEVELOPMENT.md)
- [Deployment Guide](DEPLOYMENT.md)
- [Security Guide](SECURITY.md)
- [Architecture Documentation](ARCHITECTURE.md)

---

**Still having issues?** Create a detailed issue on GitHub with all the diagnostic information above.
