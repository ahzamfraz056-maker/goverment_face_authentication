# Quick Start Guide

Get your Government Face Authentication system up and running in 5 steps.

## Step 1: Install Dependencies

```bash
npm install
```

## Step 2: Configure Back4App

1. Create a Back4App account at https://www.back4app.com/
2. Create a new app
3. Copy your **App ID** and **JavaScript Key** from App Settings

## Step 3: Update Configuration

Edit `src/app/services/parse.service.ts`:

```typescript
const APP_ID = 'your-app-id-here';
const JS_KEY = 'your-js-key-here';
```

## Step 4: Set Up Backend

Follow the detailed instructions in `BACK4APP_SETUP.md` to:
- Create Parse classes
- Configure CLPs
- Deploy Cloud Code

## Step 5: Run Locally

```bash
npm start
```

Visit `http://localhost:4200` and test the application!

## Next Steps

- **Deploy to Production**: See `DEPLOYMENT.md`
- **Full Documentation**: See `README.md`
- **Backend Setup**: See `BACK4APP_SETUP.md`

## Common Issues

### Parse SDK Not Loading
- Ensure the Parse CDN script is in `index.html` (it should be already)
- Check browser console for errors

### Camera Not Working
- Use HTTPS (required for camera access)
- Check browser permissions
- Test in Chrome or Firefox

### Cloud Code Errors
- Verify all Parse classes are created
- Check Cloud Code logs in Back4App dashboard
- Ensure CLPs are configured correctly

## Need Help?

1. Check the detailed guides:
   - `BACK4APP_SETUP.md` for backend configuration
   - `DEPLOYMENT.md` for deployment instructions
   - `README.md` for full documentation

2. Verify your setup:
   - App ID and JS Key are correct
   - All Parse classes are created
   - Cloud Code is deployed
   - CLPs are configured

3. Check browser console for errors

## Production Checklist

Before deploying to production:

- [ ] Replace placeholder face recognition with production library
- [ ] Configure HTTPS
- [ ] Set up proper CORS
- [ ] Enable email verification
- [ ] Test all features thoroughly
- [ ] Review security considerations in README.md

