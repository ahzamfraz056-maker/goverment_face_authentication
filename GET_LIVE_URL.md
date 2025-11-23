# Get Your Live HTTPS URL

Your app is built and ready to deploy! Here's how to get your live HTTPS URL:

## Step 1: Deploy to Back4App Web Hosting

1. **Log in to Back4App Dashboard**
   - Go to https://www.back4app.com/
   - Log in to your account

2. **Navigate to Your App**
   - Select your app from the dashboard
   - If you don't have an app yet, create one first

3. **Go to Web Hosting**
   - In your app dashboard, click on **"Web Hosting"** in the left sidebar
   - Or go to: App Settings → Web Hosting

4. **Upload Your Files**
   - Click **"Upload Files"** or drag and drop
   - Select ALL files from: `dist/government-face-auth` folder
   - Wait for upload to complete

## Step 2: Get Your Live URL

After uploading, your app will be available at:

```
https://[YOUR-APP-NAME].back4app.io
```

**To find your app name:**
- Check your Back4App dashboard URL
- Or go to: App Settings → General → App Name
- Your URL will be: `https://[app-name].back4app.io`

## Step 3: Important Before Testing

⚠️ **Before testing face authentication, make sure:**

1. **Back4App is configured:**
   - Update `src/app/services/parse.service.ts` with your App ID and JS Key
   - Rebuild: `npm run build:prod`
   - Re-upload files

2. **Cloud Code is deployed:**
   - Copy `cloud/main.js` to Back4App Cloud Code
   - Deploy Cloud Code

3. **Parse Classes are created:**
   - See `BACK4APP_SETUP.md` for details

## Quick Test

Once deployed, visit your URL and:
1. Sign up a new account
2. Go to Dashboard
3. Enroll your face (camera will request permission)
4. Test face login

## Your Live URL Format

```
https://[your-app-name].back4app.io
```

Replace `[your-app-name]` with your actual Back4App app name.

## Need Help?

- Check `DEPLOYMENT.md` for detailed deployment steps
- Check `BACK4APP_SETUP.md` for backend configuration
- Your app files are ready in: `dist/government-face-auth`

