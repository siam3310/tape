# Quick Start: Deploy to Vercel in 3 Steps 🚀

New to deployment? Follow these 3 simple steps to get your Tape instance live!

## Step 1: Get Your Accounts Ready (5 minutes)

1. **Create a GitHub account** (if you don't have one)
   - Go to https://github.com/signup
   - Follow the signup process

2. **Fork this repository**
   - Click the "Fork" button at the top right of this page
   - This creates your own copy of the project

3. **Create a Vercel account**
   - Go to https://vercel.com/signup
   - Click "Continue with GitHub"
   - Authorize Vercel to access your GitHub repositories

## Step 2: Deploy Your App (2 minutes)

1. **Go to your Vercel Dashboard**
   - Visit https://vercel.com/dashboard
   - Click "Add New..." → "Project"

2. **Import Your Repository**
   - Find your forked `tape` repository in the list
   - Click "Import"

3. **Configure the Project**
   - **Framework Preset:** Select "Next.js"
   - **Root Directory:** Click "Edit" and select `apps/web`
   - Leave other settings as default (the vercel.json will handle them)
   - Click "Deploy"

## Step 3: Wait & Celebrate! (2-3 minutes)

- Vercel will now build and deploy your app
- You'll see a progress screen - this is normal!
- When it's done, you'll see "🎉 Congratulations!"
- Click "Visit" to see your live app!

---

## 🎯 What You Just Deployed

You deployed the **main web application** - the core Tape video platform!

## 🔗 Your Live URL

Vercel gives you a URL like: `https://your-project-name.vercel.app`

You can:
- Share this URL with others
- Set up a custom domain later (in Vercel settings)
- Get automatic deployments when you push changes to GitHub

## 🆘 Something Went Wrong?

**Build failed?** 
- Check the detailed guide: [DEPLOYMENT.md](DEPLOYMENT.md)
- Most issues are solved by checking the build logs in Vercel

**Need more help?**
- Read the full [Deployment Guide](DEPLOYMENT.md)
- Join our [Discord community](https://tape.xyz/discord)
- Check [Vercel's documentation](https://vercel.com/docs)

## 📚 Next Steps

Want to deploy the other apps too?

- **Embed Player** → Follow the same steps but select `apps/embed` as root directory
- **OG Generator** → Follow the same steps but select `apps/og` as root directory

See the full [DEPLOYMENT.md](DEPLOYMENT.md) guide for more details!

---

**That's it!** You just deployed a complex web application. Great job! 👏
