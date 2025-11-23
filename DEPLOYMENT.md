# Deployment Guide

This guide will help you deploy the Government Face Authentication application to Back4App Web Hosting.

## Prerequisites

1. Back4App account with an app created
2. Backend configured (see `BACK4APP_SETUP.md`)
3. Cloud Code deployed
4. App ID and JS Key configured in `parse.service.ts`

## Step 1: Build the Application

Build the Angular application for production:

```bash
npm run build:prod
```

This will create optimized production files in the `dist/government-face-auth` directory.

## Step 2: Prepare for Deployment

1. **Verify Build Output**
   - Check that `dist/government-face-auth` contains:
     - `index.html`
     - `main-[hash].js`
     - `styles-[hash].css`
     - Other assets

2. **Verify Configuration**
   - Ensure `src/app/services/parse.service.ts` has your actual App ID and JS Key
   - Rebuild if you made changes: `npm run build:prod`

## Step 3: Deploy to Back4App Web Hosting

### Option A: Using Back4App Dashboard

1. **Access Web Hosting**
   - Log in to your Back4App dashboard
   - Navigate to your app
   - Go to **Web Hosting** section

2. **Upload Files**
   - Click **Upload Files** or drag and drop
   - Select ALL files from `dist/government-face-auth` folder
   - Wait for upload to complete

3. **Verify Deployment**
   - Your app will be available at: `https://your-app-name.back4app.io`
   - Visit the URL to verify it's working

### Option B: Using Back4App CLI (if available)

```bash
# Install Back4App CLI (if available)
npm install -g back4app-cli

# Login
back4app login

# Deploy
back4app deploy dist/government-face-auth
```

## Step 4: Configure CORS (if needed)

If you encounter CORS errors:

1. Go to **App Settings** → **Security**
2. Add your domain to allowed origins
3. Or enable "Allow all origins" for development (not recommended for production)

## Step 5: Test Deployment

1. **Test Basic Functionality**
   - Visit your deployed URL
   - Test sign up
   - Test password login
   - Test face enrollment (requires HTTPS)

2. **Test Face Authentication**
   - Ensure you're using HTTPS (required for camera access)
   - Test face enrollment
   - Test face login

3. **Check Console**
   - Open browser developer tools
   - Check for any errors in console
   - Verify Parse SDK is loading correctly

## Step 6: Environment-Specific Configuration

### Development
- Use `npm start` for local development
- Point to your Back4App development app

### Production
- Build with `npm run build:prod`
- Deploy to Back4App Web Hosting
- Use production Back4App app

## Troubleshooting

### Build Errors

**Error: Module not found**
```bash
# Clear cache and reinstall
rm -rf node_modules package-lock.json
npm install
```

**Error: TailwindCSS not working**
```bash
# Ensure TailwindCSS is installed
npm install -D tailwindcss@^3.4.0 postcss autoprefixer
```

### Deployment Errors

**404 Errors**
- Ensure `index.html` is in the root of uploaded files
- Check that all asset paths are correct

**Parse SDK Not Loading**
- Verify Parse CDN script is in `index.html`
- Check browser console for script loading errors

**CORS Errors**
- Configure CORS in Back4App dashboard
- Ensure your domain is in allowed origins

**Camera Not Working**
- HTTPS is required for camera access
- Check browser permissions
- Test in different browsers

### Runtime Errors

**Authentication Errors**
- Verify App ID and JS Key are correct
- Check Cloud Code is deployed
- Verify Parse classes exist

**Face Recognition Errors**
- Ensure face recognition is properly implemented
- Check Cloud Code logs in Back4App dashboard

## Post-Deployment Checklist

- [ ] Application loads correctly
- [ ] Sign up works
- [ ] Password login works
- [ ] Face enrollment works (if implemented)
- [ ] Face login works (if implemented)
- [ ] Dashboard loads for authenticated users
- [ ] Admin panel accessible (for admins)
- [ ] Officer console accessible (for officers)
- [ ] Access logs are being created
- [ ] Audit logs are being created
- [ ] No console errors
- [ ] Mobile responsive design works

## Security Checklist

- [ ] HTTPS is enabled
- [ ] API keys are not exposed in client code
- [ ] CORS is properly configured
- [ ] Rate limiting is implemented (if needed)
- [ ] Face recognition is production-ready (not placeholder)

## Monitoring

1. **Back4App Dashboard**
   - Monitor Cloud Code logs
   - Check API usage
   - Monitor error rates

2. **Application Logs**
   - Check browser console for client-side errors
   - Monitor access sessions in admin panel
   - Review audit logs regularly

## Updates and Maintenance

### Updating the Application

1. Make changes to source code
2. Rebuild: `npm run build:prod`
3. Upload new files to Back4App Web Hosting
4. Clear browser cache if needed

### Updating Cloud Code

1. Make changes to `cloud/main.js`
2. Deploy via Back4App Cloud Code dashboard
3. Test thoroughly

## Support

For deployment issues:
1. Check Back4App documentation
2. Review browser console errors
3. Check Back4App Cloud Code logs
4. Verify all configuration steps in `BACK4APP_SETUP.md`

