# Pre-Deployment Verification Checklist

## ✅ Code Quality & Security

- [ ] **No hardcoded secrets**: Run `grep -r "GEMINI_API_KEY\|SMTP_PASS\|SECRET" src/` and verify no actual keys in code
- [ ] **No console.logs in production code**: Check `src/` for debug logs
- [ ] **TypeScript compiles**: Run `npm run lint` without errors
- [ ] **No unused dependencies**: Review `package.json` for unused packages

## ✅ Git & GitHub Setup

- [ ] **GitHub repository created**
- [ ] **Repository is public** (if you want others to find it)
- [ ] **Remote added**: Run `git remote -v` to verify
- [ ] **All changes committed**: Run `git status` shows clean working directory
- [ ] **No sensitive files in git**: Verify `.gitignore` excludes `.env*` files

### Verify No Secrets Committed
```bash
# Check if any .env files were accidentally committed
git log -p -- '.env*' | head

# Check git history for API keys (look for patterns)
git log -p | grep -i "api_key\|password" || echo "No obvious secrets found"
```

## ✅ Environment Files

- [ ] **`.env.example` updated**: Contains all required variables (GEMINI_API_KEY, SMTP_*)
- [ ] **`.env.local` exists locally**: Has actual values (never commit this)
- [ ] **No `.env` or `.env.local` in git**: Run `git ls-files | grep env` (should show none)

## ✅ Configuration Files

- [ ] **`package.json`**: Build scripts correct (`npm run build` works)
- [ ] **`vite.config.ts`**: Proper environment variable handling
- [ ] **`vercel.json`**: Routes configured for SPA (fallback to index.html)
- [ ] **`tsconfig.json`**: TypeScript target is ES2022

## ✅ Build & Runtime Tests

```bash
# Install dependencies fresh
npm install

# Run type checking
npm run lint

# Build for production
npm run build

# Verify build output exists
ls -la dist/ | head -5

# Test that build is small enough
du -sh dist/
```

- [ ] **Build succeeds** without errors
- [ ] **Build size reasonable** (typically < 500KB for React app)
- [ ] **No build warnings** (or documented and acceptable)

## ✅ API Routes & Backend

- [ ] **Express routes defined**: `server.ts` has `/api/notify` endpoint
- [ ] **Error handling implemented**: Server handles missing env vars gracefully
- [ ] **SMTP fallback works**: Server logs emails to console if SMTP not configured
- [ ] **Port configurable**: Server uses `process.env.PORT` or default 3000

## ✅ Frontend Components

- [ ] **No API keys in components**: Check `src/components/` for hardcoded secrets
- [ ] **API calls use relative paths**: `/api/notify` not `http://localhost:3000/api/notify`
- [ ] **Logo reference updated**: `public/logo.png` exists or update references
- [ ] **No localhost references**: Search for `localhost:3000` in code

## ✅ Documentation

- [ ] **README.md updated**: Clear instructions for running locally and deploying
- [ ] **GITHUB_DEPLOYMENT.md exists**: Step-by-step deployment guide
- [ ] **LOGIN_INFO.md includes test accounts**: For testing after deployment
- [ ] **.env.example has comments**: Explaining each variable

## ✅ Vercel-Specific Setup

- [ ] **Vercel account created**: https://vercel.com
- [ ] **GitHub connected to Vercel**: Account → Integrations
- [ ] **Project will auto-detect settings**: Framework = Vite, Output = dist
- [ ] **Environment variables ready to add**: Have GEMINI_API_KEY, SMTP vars ready

## ✅ Final GitHub Push

```bash
# Verify clean status
git status

# Create new branch for final checks (optional)
git checkout -b deploy/prepare-github

# Add all changes
git add .

# Commit with clear message
git commit -m "Prepare project for GitHub deployment - add deployment docs and CI/CD workflows"

# Push to GitHub
git push origin main

# Or if using branch
git push origin deploy/prepare-github
```

- [ ] **All files committed**: `git status` shows "nothing to commit"
- [ ] **Pushed to GitHub**: Code visible on github.com
- [ ] **Workflows visible**: GitHub → Actions shows workflows

## ✅ After GitHub Push - Vercel Setup

1. [ ] **Go to Vercel**: https://vercel.com/new
2. [ ] **Import GitHub Project**: Select your repository
3. [ ] **Vercel detects settings**: Should auto-detect Vite
4. [ ] **Add Environment Variables**:
   - [ ] `GEMINI_API_KEY`
   - [ ] `SMTP_HOST`
   - [ ] `SMTP_PORT`
   - [ ] `SMTP_USER`
   - [ ] `SMTP_PASS`
   - [ ] `EMAIL_FROM`
5. [ ] **Deploy**: Click Deploy button
6. [ ] **Test deployment**:
   - [ ] App loads without 404s
   - [ ] Login page displays
   - [ ] No console errors in browser DevTools

## ✅ Troubleshooting

### If build fails:
```bash
npm run lint     # Check TypeScript
npm run build    # Rebuild locally
```

### If deployable size too large:
- Check `dist/` for unnecessary files
- Run `npm run clean` before build
- Remove unused dependencies from `package.json`

### If API returns 404:
- Verify `vercel.json` exists and is valid JSON
- Check Express routes in `server.ts`
- Verify backend environment variables in Vercel dashboard

## 🎉 Success Indicators

- ✅ GitHub repository shows code
- ✅ Vercel deployment shows "Ready"
- ✅ App URL accessible and working
- ✅ GitHub Actions workflows run successfully
- ✅ CI badge shows passing status

---

**Ready for deployment?** Follow these steps:
1. Complete all checklist items above
2. Push to GitHub
3. Connect to Vercel
4. Configure environment variables
5. Deploy and test!
