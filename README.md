<div align="center">
<img width="1200" height="475" alt="GHBanner" src="https://github.com/user-attachments/assets/0aa67016-6eaf-458a-adb2-6e31a0763ed6" />
</div>

# EGTC Staff Pro - Medical Treatment System

A modern React-based staff management system with Gemini AI integration and email notifications.

View your app in AI Studio: https://ai.studio/apps/ebb655dc-31ed-4897-8261-012272e4ca3b

## 📋 Overview

**Tech Stack**:
- Frontend: React 19 + Vite + TypeScript + Tailwind CSS
- Backend: Express.js
- AI Integration: Google Gemini API
- Email: Nodemailer with SMTP support

## 🚀 Quick Start - Run Locally

**Prerequisites**: Node.js 18+ required

1. **Install dependencies**:
   ```bash
   npm install
   ```

2. **Setup environment variables** - Create `.env.local` based on `.env.example`:
   ```bash
   cp .env.example .env.local
   ```
   
   Then edit `.env.local` and add:
   - `GEMINI_API_KEY` - Get from [Google AI Studio](https://aistudio.google.com)
   - `SMTP_*` variables (optional, for email notifications)

3. **Start development server**:
   ```bash
   npm run dev
   ```
   Server runs on `http://localhost:3000`

4. **Build for production**:
   ```bash
   npm run build
   npm run preview
   ```

## 🌐 Deployment

### Quick Deploy to Vercel (Recommended)

1. Push code to GitHub
2. Go to [Vercel](https://vercel.com) → Import Project
3. Select your GitHub repository
4. Add environment variables in Vercel dashboard
5. Deploy!

**See [GITHUB_DEPLOYMENT.md](./GITHUB_DEPLOYMENT.md) for detailed deployment instructions.**

### GitHub Actions CI/CD

Automated builds run on every push. Workflows:
- `.github/workflows/build.yml` - Type check and build verification
- `.github/workflows/deploy-vercel.yml` - Auto-deploy to Vercel (requires setup)

## 📁 Project Structure

```
├── src/               # React frontend
│   ├── components/    # React components
│   ├── contexts/      # React contexts (Auth, Notifications)
│   └── services/      # API & DB services
├── api/               # Backend API routes
├── server.ts          # Express server setup
├── vite.config.ts     # Vite configuration
└── vercel.json        # Vercel routing configuration
```

## 🔐 Environment Variables

Copy `.env.example` to `.env.local` and configure:

```env
# Required
GEMINI_API_KEY=your_key_here

# Optional (for email notifications)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your_email@gmail.com
SMTP_PASS=your_app_password
EMAIL_FROM=EGTC Staff Pro <noreply@example.com>
```

## 📝 Available Scripts

| Command | Purpose |
|---------|---------|
| `npm run dev` | Start dev server with hot reload |
| `npm run build` | Build for production |
| `npm run preview` | Preview production build |
| `npm run lint` | TypeScript type checking |
| `npm run clean` | Remove build artifacts |

## 🔗 Resources

- [Deployment Guide](./GITHUB_DEPLOYMENT.md)
- [Login Credentials](./LOGIN_INFO.md)
- [System Requirements](./DEPLOYMENT.md)
- [Vercel Docs](https://vercel.com/docs)
- [Vite Docs](https://vitejs.dev)
