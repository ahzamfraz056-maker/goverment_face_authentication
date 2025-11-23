# Back4App Setup Guide

This guide will help you set up the Back4App backend for the Government Face Authentication application.

## Prerequisites

1. A Back4App account (sign up at https://www.back4app.com/)
2. Your Back4App App ID and JavaScript Key

## Step 1: Create Back4App Application

1. Log in to your Back4App dashboard
2. Click "Create a new app"
3. Choose a name for your app (e.g., "Government Face Auth")
4. Note down your **App ID** and **JavaScript Key** from the App Settings

## Step 2: Configure Parse Classes

Create the following classes in your Back4App dashboard:

### 1. CitizenProfile
Fields:
- `user` (Pointer to _User) - Required
- `fullName` (String) - Required
- `govId` (String) - Required, Unique
- `department` (String) - Required
- `role` (Array) - Default: ["citizen"]

### 2. FaceTemplate
Fields:
- `user` (Pointer to _User) - Required
- `imageUrl` (String) - Required
- `embedding` (Array) - Required
- `isActive` (Boolean) - Default: true

### 3. AccessSession
Fields:
- `user` (Pointer to _User) - Optional (for failed logins)
- `method` (String) - Values: "password", "face"
- `status` (String) - Values: "success", "failed"
- `ipAddress` (String)
- `deviceInfo` (String)

### 4. AuditLog
Fields:
- `actor` (Pointer to _User) - Required
- `action` (String) - Required
- `meta` (Object) - Optional

## Step 3: Configure Class Level Permissions (CLPs)

### CitizenProfile CLPs
- **Read**: Owner, Role: Officer, Role: Admin
- **Create**: Authenticated users
- **Update**: Owner, Role: Admin
- **Delete**: Role: Admin

### FaceTemplate CLPs
- **Read**: Owner, Role: Admin
- **Create**: Authenticated users
- **Update**: Owner, Role: Admin
- **Delete**: Owner, Role: Admin

### AccessSession CLPs
- **Read**: Owner, Role: Admin
- **Create**: Cloud Code only (uncheck all boxes)
- **Update**: Role: Admin
- **Delete**: Role: Admin

### AuditLog CLPs
- **Read**: Role: Admin
- **Create**: Cloud Code only (uncheck all boxes)
- **Update**: None
- **Delete**: None

## Step 4: Create Roles

1. Go to **Core** → **Roles** in your Back4App dashboard
2. Create two roles:
   - `Officer` (name must be exactly "Officer")
   - `Admin` (name must be exactly "Admin")

## Step 5: Deploy Cloud Code

1. Go to **Cloud Code** in your Back4App dashboard
2. Copy the contents of `cloud/main.js`
3. Paste it into the Cloud Code editor
4. Click **Deploy**

**Important**: The face recognition implementation in `generateFaceEmbedding()` is a placeholder. For production, you must:

1. Integrate a proper face recognition library (e.g., face-api.js, AWS Rekognition, Azure Face API)
2. Replace the dummy embedding generation with actual face recognition
3. Adjust the similarity threshold in `loginWithFace` function

## Step 6: Configure Frontend

1. Open `src/app/services/parse.service.ts`
2. Replace `YOUR_APP_ID` with your Back4App App ID
3. Replace `YOUR_JS_KEY` with your Back4App JavaScript Key

```typescript
const APP_ID = 'your-actual-app-id';
const JS_KEY = 'your-actual-js-key';
```

## Step 7: Enable Email Verification (Optional but Recommended)

1. Go to **App Settings** → **Email Settings**
2. Configure your email service (SMTP or use Back4App's email service)
3. Enable email verification for sensitive actions

## Step 8: Test the Setup

1. Build your Angular app: `npm run build:prod`
2. Deploy to Back4App Web Hosting (see deployment section)
3. Test sign up, login, and face enrollment

## Troubleshooting

### Cloud Code Errors
- Ensure all Parse classes are created before deploying Cloud Code
- Check Cloud Code logs in Back4App dashboard for errors

### Permission Errors
- Verify CLPs are set correctly
- Ensure roles are created and users are assigned to roles

### Face Recognition Not Working
- Replace the placeholder `generateFaceEmbedding()` function with actual face recognition
- Adjust similarity threshold if needed

## Security Notes

1. **Face Recognition**: The current implementation uses a placeholder. For production, integrate a proper face recognition service.

2. **API Keys**: Never commit your App ID and JS Key to version control. Use environment variables or a config file that's gitignored.

3. **HTTPS**: Always use HTTPS in production.

4. **Rate Limiting**: Consider implementing rate limiting for login attempts.

5. **Face Template Storage**: Face embeddings are stored in Parse. Consider encrypting sensitive biometric data.

