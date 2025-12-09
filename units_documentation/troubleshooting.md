# Troubleshooting

This guide helps you diagnose and resolve common issues with the Units warehouse management system.

## Login Issues

### Problem: Cannot Login

#### Symptoms

- "Invalid email or password" error
- Login button doesn't work
- Redirected back to login after entering credentials

#### Solutions

**1. Verify Credentials**

- Check email address for typos
- Verify password (case-sensitive)
- Ensure Caps Lock is off
- Try copying and pasting credentials

**2. Check Password Requirements**
If recently changed, ensure password meets requirements:

- At least 8 characters
- One uppercase letter
- One lowercase letter
- One number
- One special character

**3. Reset Password**

- Click "Forgot Password?" on login page
- Enter your email address
- Check email for reset link
- Follow instructions to set new password

**4. Email Verification**

- Ensure your email is verified
- Check spam folder for verification email
- Request new verification email if needed

**5. Account Status**

- Contact your administrator to verify account is active
- Account may be deactivated or expired

**6. Browser Issues**

- Clear browser cache and cookies
- Try incognito/private browsing mode
- Try a different browser
- Disable browser extensions that might interfere

**7. Network Issues**

- Check internet connection
- Verify you can access the login page
- Check if firewall is blocking the API

### Problem: Session Expires Too Quickly

#### Solutions

**1. Enable "Remember Me"**

- Check "Remember Me" box at login
- Session will persist longer

**2. Check Token Expiry**

- Default expiry is set by backend
- Contact administrator to adjust if needed

**3. Keep Tab Active**

- Inactive sessions may timeout
- Refresh page periodically if idle

## Data Loading Issues

### Problem: Pages Load Slowly or Show Errors

#### Symptoms

- Infinite loading spinners
- "Failed to fetch data" errors
- Blank pages
- Slow performance

#### Solutions

**1. Check Internet Connection**

```bash
# Test API connectivity
curl https://api.units.abc.com/api/health
```

**2. Clear Browser Cache**

- Chrome: Ctrl+Shift+Delete → Clear browsing data
- Firefox: Ctrl+Shift+Delete → Clear recent history
- Safari: Safari menu → Clear History

**3. Check API Status**

- Verify backend API is running
- Contact system administrator
- Check status page (if available)

**4. Browser Console Errors**

- Press F12 to open developer tools
- Check Console tab for errors
- Report errors to administrator

**5. Refresh the Page**

- Press F5 or Ctrl+R
- Hard refresh: Ctrl+Shift+R

**6. Check Date Range Filters**

- Overly broad date ranges may timeout
- Narrow the date range
- Use pagination

### Problem: Data Not Updating

#### Symptoms

- Changes don't appear after saving
- Old data still shows
- Dashboard metrics not current

#### Solutions

**1. Refresh Page**

- Press F5 to reload
- Log out and log back in

**2. Check Save Confirmation**

- Ensure you see success message
- Check for error messages
- Verify form validation passed

**3. Wait for Processing**

- Some operations take time
- Check back after a few minutes
- Look for status updates

**4. Check Permissions**

- Verify you have write access
- Some fields may be read-only
- Contact administrator if needed

## Form and Input Issues

### Problem: Cannot Submit Form

#### Symptoms

- Submit button disabled
- Form validation errors
- Nothing happens when clicking submit

#### Solutions

**1. Check Required Fields**

- Look for asterisk (\*) next to field labels
- All required fields must be filled
- Red borders indicate missing/invalid fields

**2. Fix Validation Errors**

- Read error messages below fields
- Correct invalid data (e.g., email format)
- Ensure numbers are in valid range

**3. Check Field Formats**

- Dates: Use date picker, don't type
- Numbers: No letters or special characters
- Email: Must include @
- Phone: Follow expected format

**4. Try Again**

- Close and reopen the form
- Refresh the page
- Log out and back in

### Problem: File Upload Fails

#### Symptoms

- "Upload failed" error
- File not appearing after upload
- Image not displaying

#### Solutions

**1. Check File Size**

- Maximum file size: Usually 5-10MB
- Compress large images before upload
- Use JPEG for photos (smaller than PNG)

**2. Check File Format**

- Allowed formats: JPG, PNG, PDF, Excel
- Rename file if unusual characters in name
- Remove spaces from filename

**3. Check Internet Speed**

- Large files need good connection
- Wait for upload to complete
- Don't navigate away during upload

**4. Try Different Browser**

- Some browsers handle uploads differently
- Chrome usually most reliable

## Search and Filter Issues

### Problem: Search Not Finding Results

#### Symptoms

- No results when searching
- Expected items not appearing
- Search seems to not work

#### Solutions

**1. Check Search Term**

- Remove extra spaces
- Try partial match (fewer characters)
- Try different keywords
- Check spelling

**2. Check Filters**

- Clear all filters and try again
- Filters may be too restrictive
- Date range may exclude items

**3. Check Status Filters**

- Item may be in different status
- Check all status tabs
- Include completed/archived items

**4. Verify Data Exists**

- Item may not be created yet
- Check with administrator
- Verify you have access to the data

## Performance Issues

### Problem: Application Runs Slowly

#### Symptoms

- Pages load slowly
- Lag when typing
- Delayed button clicks
- Browser becomes unresponsive

#### Solutions

**1. Close Unnecessary Tabs**

- Too many tabs use memory
- Close other applications
- Restart browser

**2. Clear Browser Cache**

- Accumulated cache slows performance
- Clear cookies and cache
- Restart browser

**3. Check Browser Extensions**

- Disable extensions temporarily
- Some extensions cause slowdowns
- Use incognito mode to test

**4. Update Browser**

- Use latest browser version
- Old browsers are slower
- Security updates improve performance

**5. Check Computer Resources**

- Close other applications
- Restart computer
- Check CPU and memory usage

**6. Optimize Date Ranges**

- Don't load huge date ranges
- Use specific date filters
- Paginate results

## Barcode and Scanning Issues

### Problem: Barcode Scanner Not Working

#### Symptoms

- Scanner not reading barcodes
- Scanned data not appearing
- Wrong data being entered

#### Solutions

**1. Check Scanner Connection**

- USB scanner: Check cable and port
- Bluetooth scanner: Check pairing
- Test scanner in notepad first

**2. Check Scanner Configuration**

- Scanner may need keyboard wedge mode
- Verify barcode format supported
- Check scanner manual

**3. Focus on Input Field**

- Click in the barcode input field
- Scanner must have cursor focus
- Try clicking then scanning

**4. Barcode Quality**

- Ensure barcode is clear and not damaged
- Clean barcode if dirty
- Try different lighting
- Manually enter if needed

**5. Browser Compatibility**

- Some scanners work better in specific browsers
- Try Chrome if having issues

## Report Issues

### Problem: Report Not Generating

#### Symptoms

- Report shows no data
- Error when generating report
- Timeout error

#### Solutions

**1. Check Date Range**

- Large date ranges may timeout
- Narrow the date range
- Try smaller periods

**2. Check Filters**

- Remove some filters
- Ensure filters have matching data
- Try "All" options

**3. Wait Longer**

- Large reports take time
- Don't close window
- Check back after few minutes

**4. Export to Excel**

- If PDF fails, try Excel
- Excel may handle large data better
- Process offline

**5. Contact Administrator**

- May need to generate server-side
- Request scheduled report
- Ask for database query

## Integration Issues

### Problem: Google Maps Not Loading

#### Symptoms

- Address picker not working
- Map shows blank or error
- "Map cannot load" message

#### Solutions

**1. Check API Key**

- Verify Google Maps API key configured
- Contact administrator if error persists

**2. Check Internet Connection**

- Maps require good connection
- Check if other sites with maps work

**3. Check Browser Console**

- F12 → Console tab
- Look for Maps API errors
- Report to administrator

### Problem: Salla Integration Not Working

#### Symptoms

- Orders not importing from Salla
- Authorization fails
- Connection error

#### Solutions

**1. Reauthorize Connection**

- Go to Salla integration settings
- Click "Authorize" again
- Follow OAuth flow

**2. Check Salla Status**

- Verify Salla store is active
- Check Salla account permissions

**3. Contact Administrator**

- Integration may need reconfiguration
- Check logs for errors

## Mobile and Tablet Issues

### Problem: Interface Not Responsive

#### Symptoms

- Layout broken on mobile
- Can't access buttons
- Text too small or overlapping

#### Solutions

**1. Rotate Device**

- Try landscape orientation
- Some pages work better landscape

**2. Zoom Out**

- Pinch to zoom out
- May reveal hidden elements

**3. Use Latest Browser**

- Update mobile browser
- Try Chrome on Android
- Try Safari on iOS

**4. Clear Mobile Browser Cache**

- Settings → Browser → Clear data

**5. Use Desktop Site**

- Some tasks better on desktop
- Remote desktop if available

## Language Issues

### Problem: Wrong Language Showing

#### Solutions

**1. Change Language**

- Click language selector (EN/AR)
- Choose preferred language
- Setting is saved

**2. Clear Browser Cache**

- Language preference in cache
- Clear and select again

**3. Check Browser Language**

- May auto-detect browser language
- Override in settings

### Problem: Text Not Translated

#### Solutions

**1. Refresh Page**

- Language switch may need refresh
- Hard refresh: Ctrl+Shift+R

**2. Report Missing Translations**

- Some text may not be translated yet
- Contact administrator
- Provide context and location

## Error Messages

### Common Error Messages and Solutions

#### "Invalid Token Access"

- **Cause**: Session expired or invalid
- **Solution**: Log out and log back in

#### "User Not Found"

- **Cause**: Account doesn't exist or deleted
- **Solution**: Verify email, contact administrator

#### "SKU Code Already Exists"

- **Cause**: Duplicate SKU code
- **Solution**: Use unique SKU code

#### "Insufficient Permissions"

- **Cause**: User role doesn't allow this action
- **Solution**: Contact administrator for access

#### "Network Error"

- **Cause**: Cannot reach API server
- **Solution**: Check internet, verify API status

#### "Failed to Fetch"

- **Cause**: API not responding or network issue
- **Solution**: Check connection, refresh, contact administrator

## Browser-Specific Issues

### Chrome Issues

**Console Errors**

- F12 → Console tab → Check errors
- Report to administrator

**Clear Cache**

- Settings → Privacy → Clear browsing data
- Check "Cached images and files"
- Clear from "All time"

### Firefox Issues

**Console Errors**

- F12 → Console → Check errors

**Clear Cache**

- Settings → Privacy → Clear Data
- Check "Cached Web Content"

### Safari Issues

**Console Errors**

- Develop menu → Show Web Inspector

**Clear Cache**

- Safari → Clear History
- Choose "All history"

## Getting More Help

### Information to Provide

When reporting an issue, include:

1. **What you were doing** - Step by step
2. **What you expected** - What should happen
3. **What actually happened** - The error or issue
4. **When it happened** - Date and time
5. **Screenshots** - If applicable
6. **Browser and version** - Chrome 120, etc.
7. **Error messages** - Exact text
8. **Username** - For admin to check logs
9. **Device type** - Desktop, tablet, mobile

### Where to Get Help

1. **Documentation**: Check relevant docs first
2. **FAQ**: See [FAQ](./faq.md) for common questions
3. **Administrator**: Contact your system admin
4. **Support Email**: support@units.abc.com
5. **Training**: Request additional training

### Emergency Contact

For critical production issues:

- Contact your system administrator immediately
- Provide severity level: Critical, High, Medium, Low
- Describe business impact

## Preventive Measures

### Best Practices to Avoid Issues

1. **Keep Browser Updated** - Latest version
2. **Clear Cache Regularly** - Once a month
3. **Save Work Frequently** - Don't rely on autosave
4. **Use Strong Internet** - Stable connection
5. **Log Out Properly** - Don't just close tab
6. **Report Issues Early** - Don't wait for critical failure
7. **Follow Training** - Use system as designed
8. **Backup Important Data** - Export reports regularly
9. **Use Recommended Browser** - Chrome preferred
10. **Stay Informed** - Read system announcements

## Next Steps

- Review [User Guide](./user-guide.md) for proper usage
- Check [FAQ](./faq.md) for common questions
- See [Configuration](./configuration.md) for setup issues
