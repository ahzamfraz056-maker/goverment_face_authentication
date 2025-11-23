# Government Face Authentication System

A government-grade face authentication web application built with Angular, TypeScript, TailwindCSS, and Back4App (Parse) backend.

## Features

- 🔐 **Password Authentication**: Traditional username/password login
- 👤 **Face Authentication**: Secure face-based login using facial recognition
- 👥 **User Management**: Citizen profiles with government ID tracking
- 📊 **Access Logging**: Comprehensive access session tracking
- 🔍 **Audit Logs**: Complete audit trail of all system actions
- 👮 **Officer Console**: Read-only access to citizen verification
- ⚙️ **Admin Panel**: Full user management and system monitoring
- 📱 **Responsive Design**: Mobile-friendly government-style UI

## Tech Stack

- **Frontend**: Angular 17, TypeScript, TailwindCSS 3.4.0
- **Backend**: Back4App (Parse Server)
- **Face Recognition**: Placeholder implementation (requires production face recognition library)
- **Deployment**: Back4App Web Hosting

## Prerequisites

- Node.js 18+ and npm
- Back4App account
- Modern web browser with camera support (for face authentication)

## Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd government-face-auth
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Configure Back4App**
   - Follow the instructions in `BACK4APP_SETUP.md`
   - Update `src/app/services/parse.service.ts` with your App ID and JS Key

4. **Build the application**
   ```bash
   npm run build:prod
   ```

5. **Deploy to Back4App Web Hosting**
   - Upload the contents of `dist/government-face-auth` to Back4App Web Hosting
   - See deployment section below

## Development

Run the development server:

```bash
npm start
```

The app will be available at `http://localhost:4200`

## Project Structure

```
src/
├── app/
│   ├── components/
│   │   ├── admin/          # Admin panel components
│   │   ├── dashboard/      # Dashboard components
│   │   ├── face/           # Face enrollment component
│   │   ├── layout/         # Header component
│   │   └── officer/        # Officer console components
│   ├── guards/             # Route guards (auth, role)
│   ├── pages/              # Page components
│   ├── services/           # Services (auth, parse)
│   └── app.routes.ts       # Route configuration
├── index.html
├── main.ts
└── styles.css
```

## Backend Setup

See `BACK4APP_SETUP.md` for detailed backend configuration instructions.

### Required Parse Classes

1. **CitizenProfile**: User profile with government ID
2. **FaceTemplate**: Face embeddings for authentication
3. **AccessSession**: Login attempt tracking
4. **AuditLog**: System audit trail

### Cloud Code Functions

- `signUpCitizen`: Create new citizen account
- `loginWithPassword`: Password-based login
- `enrollFace`: Enroll face template
- `loginWithFace`: Face-based authentication
- `setUserRole`: Admin function to change user roles

## Deployment

### Deploy to Back4App Web Hosting

1. **Build for production**
   ```bash
   npm run build:prod
   ```

2. **Upload to Back4App**
   - Go to your Back4App dashboard
   - Navigate to **Web Hosting**
   - Upload the contents of `dist/government-face-auth` folder
   - Your app will be available at `https://your-app-name.back4app.io`

3. **Configure CORS** (if needed)
   - Ensure your Back4App app allows requests from your domain

## Usage

### For Citizens

1. **Sign Up**: Create an account with government ID
2. **Sign In**: Login with username/password or face
3. **Enroll Face**: Capture and enroll your face template
4. **View History**: Check your access history

### For Officers

1. **Search Citizens**: Search by government ID or name
2. **View Access History**: Read-only access to citizen login history

### For Admins

1. **User Management**: View and manage all users
2. **Role Management**: Assign roles (citizen, officer, admin)
3. **Access Logs**: View global access session logs
4. **Audit Logs**: View complete system audit trail

## Security Considerations

⚠️ **Important**: This is a demonstration application. For production use:

1. **Face Recognition**: Replace placeholder implementation with production-grade face recognition (AWS Rekognition, Azure Face API, etc.)
2. **API Keys**: Never commit API keys to version control
3. **HTTPS**: Always use HTTPS in production
4. **Rate Limiting**: Implement rate limiting for login attempts
5. **Biometric Data**: Consider encryption for stored face embeddings
6. **Email Verification**: Enable email verification for sensitive actions

## Face Recognition Implementation

The current face recognition implementation is a **placeholder**. To use in production:

1. Integrate a face recognition library (e.g., face-api.js, AWS Rekognition)
2. Replace `generateFaceEmbedding()` in `cloud/main.js`
3. Adjust similarity threshold as needed
4. Test thoroughly before deployment

## Troubleshooting

### Parse SDK Not Loading
- Ensure Parse CDN is loaded in `index.html`
- Check browser console for errors

### Camera Not Working
- Ensure HTTPS (required for camera access)
- Check browser permissions
- Test in different browsers

### Cloud Code Errors
- Check Back4App Cloud Code logs
- Verify all Parse classes are created
- Ensure CLPs are configured correctly

## License

This project is for demonstration purposes. Use at your own risk.

## Support

For issues and questions:
1. Check `BACK4APP_SETUP.md` for backend setup
2. Review Back4App documentation
3. Check browser console for errors

