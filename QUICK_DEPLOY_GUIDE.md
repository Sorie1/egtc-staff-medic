# Quick Deployment Reference Card

## 🎯 5-Minute GitHub & Vercel Deployment

### Phase 1: Local Verification (2 minutes)
```bash
# Test build
npm install
npm run lint
npm run build

# Verify git is clean
git status
```

### Phase 2: Push to GitHub (1 minute)
```bash
# Commit changes
git add .
git commit -m "Prepare for GitHub and Vercel deployment"
git push origin main

# OR if no remote yet:
git remote add origin https://github.com/YOUR_USERNAME/your-repo.git
git branch -M main
git push -u origin main
```

### Phase 3: Vercel Deploy (2 minutes)

#### In Vercel Dashboard:
1. Go to https://vercel.com/new
2. **Select GitHub** → **Select your repository**
3. **Framework**: Should auto-detect `Vite`
4. **Build Command**: `npm run build`
5. **Output Directory**: `dist`
6. **Add Environment Variables**:
   ```
   GEMINI_API_KEY = [your-key-from-google-ai-studio]
   SMTP_HOST = smtp.gmail.com
   SMTP_PORT = 587
   SMTP_USER = your-email@gmail.com
   SMTP_PASS = [your-gmail-app-password]
   EMAIL_FROM = EGTC Staff Pro <noreply@example.com>
   ```
7. Click **Deploy** ✅

### Phase 4: Verify Deployment (1 minute)
- ✅ Vercel shows "Ready" status
- ✅ Click URL and app loads
- ✅ No console errors (F12)
- ✅ Login page displays

---

## 🔑 Environment Variables Quick Reference

| Variable | Where to Get |
|----------|-------------|
| `GEMINI_API_KEY` | https://aistudio.google.com (Free tier available) |
| `SMTP_HOST` | Use Gmail: `smtp.gmail.com` |
| `SMTP_PORT` | Gmail uses: `587` |
| `SMTP_USER` | Your Gmail address |
| `SMTP_PASS` | Gmail App Password (not regular password) |

### Get Gmail App Password:
1. Go to https://myaccount.google.com/apppasswords
2. Select "Mail" and "Windows Computer"
3. Google generates 16-character password
4. Copy this as `SMTP_PASS`

---

## 🆘 Troubleshooting Cheat Sheet

| Problem | Solution |
|---------|----------|
| **Build fails locally** | `npm install && npm run lint` |
| **API returns 404** | Check `vercel.json` is valid JSON |
| **Env vars not working** | Redeploy Vercel after adding vars |
| **App loads but broken** | Check browser console (F12) |
| **Email not sending** | Check SMTP_PASS is app password, not regular password |
| **GitHub Actions fail** | Click Actions tab, check logs |

---

## 📊 Deployment Checklist (Before Clicking Deploy)

- [ ] `npm run build` works locally
- [ ] `npm run lint` passes (no errors)
- [ ] `git status` shows clean directory
- [ ] Code pushed to GitHub main branch
- [ ] Have all environment variables values ready
- [ ] GitHub repo is accessible

---

## 🔗 Quick Links

| Resource | Link |
|----------|------|
| Vercel Import | https://vercel.com/new |
| Google AI Studio | https://aistudio.google.com |
| Gmail App Passwords | https://myaccount.google.com/apppasswords |
| GitHub Repository | https://github.com/YOUR_USERNAME/your-repo |
| Vercel Dashboard | https://vercel.com/dashboard |

---

## 💬 What Happens After Deploy

1. **Vercel builds your code** (30-45 sec)
2. **Vercel deploys to CDN** (< 1 min)
3. **Your app is live** at `your-app.vercel.app`
4. **GitHub Actions runs** (builds & tests)
5. **Future pushes auto-deploy** if workflow enabled

---

## ✅ Success Indicators

When you see these, you're deployed:

1. ✅ Vercel dashboard shows "Ready"
2. ✅ App URL works (no 404)
3. ✅ React app loads
4. ✅ Can log in
5. ✅ No console errors
6. ✅ GitHub shows 1 repo commit

---

## 📞 Files to Read if Issues Occur

1. **How to deploy**: `GITHUB_DEPLOYMENT.md`
2. **Pre-deployment checks**: `DEPLOYMENT_CHECKLIST.md`
3. **Full status report**: `DEPLOYMENT_READINESS_REPORT.md`
4. **System docs**: `DEPLOYMENT.md`

---

## 🎉 You're All Set!

Your project is configured and ready. Following the steps above should have you deployed in **5 minutes**. 

**Start with Phase 1 → Phase 2 → Phase 3 → Phase 4**

Good luck! 🚀
