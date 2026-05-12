# GitHub Deployment Guide - EGTC Staff Pro

This guide covers deploying your React + Express application using GitHub, Vercel, and GitHub Actions.

## 📋 Project Overview

- **Frontend**: React 19 + Vite + TypeScript + Tailwind CSS
- **Backend**: Express.js with email notification API
- **Deployment Target**: Vercel (recommended) or any Node.js-compatible platform

## 🚀 Step 1: Initialize GitHub Repository

### First Time Setup
```bash
# Initialize git (if not already done)
git init

# Add all files
git add .

# Create initial commit
git commit -m "Initial commit: EGTC Staff Pro System"

# Add remote repository (replace with your repo)
git remote add origin https://github.com/your-username/egtc-staff-pro.git

# Push to GitHub
git branch -M main
git push -u origin main
```

### If Already Using Git
```bash
git add .
git commit -m "Prepare for GitHub deployment"
git push origin main
```

## 🔐 Environment Variables

### For Vercel Deployment
1. Connect your GitHub repo to Vercel
2. In Vercel Dashboard → Project Settings → Environment Variables, add:

```
GEMINI_API_KEY=your_gemini_api_key_here
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your_email@gmail.com
SMTP_PASS=your_app_password
EMAIL_FROM=EGTC Staff Pro <noreply@example.com>
NODE_ENV=production
```

### For Gmail SMTP
1. Enable 2-Factor Authentication on your Gmail account
2. Generate an App Password: https://myaccount.google.com/apppasswords
3. Use the generated 16-character password as `SMTP_PASS`

## 📦 Build & Deployment Configuration

### Build Process
- **Framework Preset**: Vite
- **Build Command**: `npm run build`
- **Output Directory**: `dist`
- **Node Version**: 18.x or higher (recommended 20.x)

### Files Already Configured
- ✅ `vercel.json` - Routes configuration for SPA
- ✅ `.gitignore` - Excludes node_modules, .env files, dist
- ✅ `package.json` - Build scripts configured
- ✅ `tsconfig.json` - TypeScript config for React
- ✅ `vite.config.ts` - Environment variable handling

## 🔄 Continuous Integration (Optional but Recommended)

A GitHub Actions workflow is included to:
- Run on every push to main branch
- Install dependencies
- Build the application
- Ensure no TypeScript errors

File: `.github/workflows/build.yml`

### Manual Testing Before Deployment
```bash
# Install dependencies
npm install

# Run type checking
npm run lint

# Build locally
npm run build

# Preview build
npm run preview
```

## 🌐 Deployment Options

### Option 1: Vercel (Recommended)
1. Go to https://vercel.com
2. Click "Import Project"
3. Select your GitHub repository
4. Vercel auto-detects Vite configuration
5. Add environment variables in dashboard
6. Deploy

### Option 2: GitHub Pages (Frontend Only)
1. Update `vite.config.ts`:
```typescript
export default defineConfig({
  base: '/egtc-staff-pro/', // Your repo name
  // ...
});
```
2. Create `.github/workflows/deploy.yml` for auto-deploy
3. Enable GitHub Pages in repo settings

### Option 3: Self-Hosted (Railway, Render, Heroku)
These platforms support Node.js applications with Express backends.

## ✅ Pre-Deployment Checklist

- [ ] All sensitive data removed from code
- [ ] `.env.example` includes all required variables
- [ ] `.gitignore` excludes `.env*` files
- [ ] No hardcoded API keys in source code
- [ ] `package.json` has correct build scripts
- [ ] TypeScript builds without errors (`npm run lint`)
- [ ] GitHub repository is created and remote is set
- [ ] Environment variables configured in Vercel
- [ ] Logo placed in `public` folder (optional)

## 🔧 Post-Deployment Verification

After deployment, verify:

1. **Frontend Loading**: App loads without 404 errors
2. **API Routes**: Test email notification at `/api/notify`
3. **Authentication**: Login page functions correctly
4. **Environment Variables**: Check console for warnings

### Test Email API
```bash
curl -X POST https://your-deployed-app.vercel.app/api/notify \
  -H "Content-Type: application/json" \
  -d '{
    "to": "test@example.com",
    "subject": "Test Email",
    "body": "This is a test notification"
  }'
```

## 🚨 Troubleshooting

### Build Fails with TypeScript Errors
```bash
npm run lint
# Fix any TypeScript issues reported
```

### Environment Variables Not Loading
- Verify variables are set in Vercel dashboard
- Check that Vercel has been redeployed after adding variables
- Ensure variable names match exactly (case-sensitive)

### API Routes Return 404
- Confirm `vercel.json` is correctly configured
- Check that Express server routes are properly defined
- Verify backend is running in production mode

### Email Notifications Not Working
- Check SMTP credentials are correct
- Verify email provider allows SMTP access
- Check server logs for error messages

## 📚 Resources

- [Vercel Documentation](https://vercel.com/docs)
- [Vite Deployment Guide](https://vitejs.dev/guide/static-deploy.html)
- [Express Deployment](https://expressjs.com/en/advanced/best-practice-deployment.html)
- [GitHub Actions](https://github.com/features/actions)

## 🎯 Next Steps

1. Push code to GitHub
2. Connect to Vercel
3. Configure environment variables
4. Monitor deployment
5. Test all features in production
