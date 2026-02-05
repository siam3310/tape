# 🚀 Deploying Tape to Vercel

This guide will help you deploy the Tape application to Vercel, even if you're new to deployment!

## 📋 Prerequisites

Before you start, make sure you have:

1. A [GitHub account](https://github.com/signup)
2. A [Vercel account](https://vercel.com/signup) (you can sign up using your GitHub account)
3. Forked this repository to your GitHub account

## 🎯 Quick Start - Deploy in 5 Minutes!

### Option 1: Deploy via Vercel Dashboard (Recommended for Beginners)

This is the easiest way to deploy your application!

1. **Sign in to Vercel**
   - Go to [vercel.com](https://vercel.com)
   - Click "Sign Up" or "Login"
   - Choose "Continue with GitHub" to connect your GitHub account

2. **Import Your Project**
   - Click the "Add New..." button in your Vercel dashboard
   - Select "Project"
   - Find and select your forked `tape` repository
   - Click "Import"

3. **Configure Your Project**
   
   Since this is a monorepo (multiple apps in one repository), you need to configure which app to deploy:

   **For the Main Web App:**
   - **Framework Preset:** Next.js
   - **Root Directory:** `apps/web`
   - **Build Command:** `cd ../.. && pnpm install && pnpm --filter @tape.xyz/web build`
   - **Output Directory:** Leave as default (`.next`)
   - **Install Command:** `cd ../.. && pnpm install`

4. **Deploy!**
   - Click "Deploy"
   - Wait for the deployment to complete (usually 2-5 minutes)
   - Once done, you'll get a live URL like `https://your-project.vercel.app`

🎉 **Congratulations!** Your app is now live!

### Option 2: Deploy via Vercel CLI

For developers who prefer the command line:

1. **Install Vercel CLI**
   ```bash
   npm i -g vercel
   ```

2. **Login to Vercel**
   ```bash
   vercel login
   ```

3. **Deploy**
   
   Navigate to the app directory you want to deploy and run:
   
   ```bash
   # For the main web app
   cd apps/web
   vercel
   
   # For the embed player
   cd apps/embed
   vercel
   
   # For the OG image generator
   cd apps/og
   vercel
   ```

4. **Follow the prompts:**
   - Set up and deploy? `Y`
   - Which scope? Choose your account
   - Link to existing project? `N`
   - Project name? Press Enter or choose a name
   - Directory? Press Enter (should auto-detect)
   - Override settings? `N` (the vercel.json will handle this)

## 📱 What Can You Deploy?

This monorepo contains multiple applications. Here's what each one does:

| App | Description | Deploy to Vercel? |
|-----|-------------|------------------|
| **web** | Main frontend application | ✅ Yes - Start here! |
| **embed** | Embed Video Player | ✅ Yes |
| **og** | Open Graph meta tags generator | ✅ Yes |
| **api** | Backend application (Hono) | ⚠️ Requires additional setup* |
| **cron** | Background cron jobs | ⚠️ Not suitable for Vercel** |

**Recommendation for beginners:** Start by deploying the **web** app first!

> *The `api` app is a Hono backend that requires database setup (Prisma) and environment configuration. While Vercel supports Node.js backends, you'll need to:
> - Set up a database (e.g., PostgreSQL on Railway, Supabase, or PlanetScale)
> - Configure database connection strings
> - Set up AWS credentials for S3/STS if needed
> - This is more advanced and recommended only after deploying the frontend successfully.

> **The `cron` app runs scheduled background tasks. Vercel's serverless functions have execution time limits (10s on Hobby, 60s on Pro), making them unsuitable for long-running cron jobs. Consider using:
> - [Vercel Cron Jobs](https://vercel.com/docs/cron-jobs) for simple scheduled tasks
> - External services like [GitHub Actions](https://docs.github.com/en/actions) or [Railway](https://railway.app/) for complex workflows

## 🔧 Environment Variables

Some features may require environment variables. To add them:

1. Go to your project in Vercel Dashboard
2. Click on "Settings"
3. Click on "Environment Variables"
4. Add any required variables (check your app's `.env.example` if it exists)

Common variables you might need:
- `NEXT_PUBLIC_API_URL` - API endpoint URL
- `NEXT_PUBLIC_ENVIRONMENT` - production/development
- Database credentials (if applicable)
- API keys for third-party services

## 🔄 Automatic Deployments

Once set up, Vercel will automatically deploy your app whenever you:
- Push to your `main` branch (production deployment)
- Create a pull request (preview deployment)

## 🐛 Troubleshooting

### Build Failed?

**Issue:** "Command failed with exit code 1"
- **Solution:** Make sure all dependencies are listed in `package.json`
- **Check:** Verify the build command is correct in vercel.json

**Issue:** "Module not found"
- **Solution:** This is a monorepo - ensure your build command includes `cd ../.. && pnpm install` to install all workspace dependencies

**Issue:** "Out of memory"
- **Solution:** You might need to upgrade to a paid Vercel plan for larger builds

### Can't Find Your Repository?

- Make sure you've granted Vercel access to your GitHub repositories
- Go to: Vercel Dashboard → Account Settings → Git Integrations → Configure GitHub

### App Not Working After Deployment?

- Check the deployment logs in Vercel Dashboard
- Verify all environment variables are set correctly
- Make sure API endpoints and external services are accessible

## 📚 Additional Resources

- [Vercel Documentation](https://vercel.com/docs)
- [Next.js Deployment Docs](https://nextjs.org/docs/deployment)
- [Monorepo Deployment Guide](https://vercel.com/docs/monorepos)
- [Tape Discord Community](https://tape.xyz/discord) - Get help from the community!

## 🆘 Need Help?

- **Vercel Issues:** Check [Vercel Support](https://vercel.com/support)
- **Project Issues:** Open an issue on [GitHub](https://github.com/tapexyz/tape/issues)
- **Community:** Join our [Discord](https://tape.xyz/discord)

## 🎓 Next Steps

After deploying successfully:

1. ✅ Set up a custom domain in Vercel settings
2. ✅ Configure environment variables for production
3. ✅ Set up other apps (embed, og) if needed
4. ✅ Enable analytics in Vercel Dashboard
5. ✅ Invite team members to collaborate

---

**Pro Tip:** Vercel's free tier is generous and perfect for getting started. You can always upgrade later as your app grows!

Happy deploying! 🎉
