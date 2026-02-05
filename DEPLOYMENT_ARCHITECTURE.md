# Deployment Architecture 🏗️

This document explains how the Tape monorepo apps can be deployed to Vercel.

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────┐
│                     Tape Monorepo                           │
│                                                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │
│  │   apps/web   │  │ apps/embed   │  │   apps/og    │     │
│  │              │  │              │  │              │     │
│  │ Main Web App │  │ Video Player │  │ OG Generator │     │
│  │  (Next.js)   │  │  (Next.js)   │  │  (Next.js)   │     │
│  └──────────────┘  └──────────────┘  └──────────────┘     │
│         │                 │                  │             │
│         └─────────────────┴──────────────────┘             │
│                          │                                  │
│                   Shared Packages                           │
│  ┌────────────────────────────────────────────────────┐    │
│  │ @tape.xyz/ui  @tape.xyz/lens  @tape.xyz/browser   │    │
│  │ @tape.xyz/constants  @tape.xyz/generic  ...       │    │
│  └────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────┘
                          │
                          ↓
┌─────────────────────────────────────────────────────────────┐
│                    Vercel Platform                          │
│                                                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │
│  │   Project 1  │  │   Project 2  │  │   Project 3  │     │
│  │              │  │              │  │              │     │
│  │   Web App    │  │    Embed     │  │      OG      │     │
│  │              │  │              │  │              │     │
│  │ tape.vercel  │  │tape-embed.   │  │ tape-og.     │     │
│  │   .app       │  │ vercel.app   │  │ vercel.app   │     │
│  └──────────────┘  └──────────────┘  └──────────────┘     │
└─────────────────────────────────────────────────────────────┘
                          │
                          ↓
                  🌍 Internet Users
```

## Deployment Strategy

### Option 1: Multiple Projects (Recommended for Production)

Deploy each app as a separate Vercel project:

- **Project 1 (Main Web)**: `apps/web` → `tape.vercel.app`
- **Project 2 (Embed)**: `apps/embed` → `tape-embed.vercel.app`  
- **Project 3 (OG)**: `apps/og` → `tape-og.vercel.app`

**Advantages:**
- Independent deployments
- Separate domain names
- Isolated environment variables
- Better performance (smaller build size per app)

**How to Deploy:**
1. Create 3 separate Vercel projects
2. Set different root directories for each
3. Each gets its own URL and deployment

### Option 2: Single Project (Simpler for Development)

Deploy just the main web app:

- **Single Project**: `apps/web` → `tape.vercel.app`

**Advantages:**
- Simpler setup (only one project)
- Good for testing/development
- Easier to manage initially

**How to Deploy:**
Follow the [Quick Start Guide](VERCEL_QUICKSTART.md)

## Build Process

For each app, Vercel will:

1. **Install Dependencies**
   ```bash
   cd ../.. && pnpm install
   ```
   This installs all workspace dependencies (monorepo requirement)

2. **Build the App**
   ```bash
   pnpm --filter @tape.xyz/<app-name> build
   ```
   This builds only the specific app

3. **Deploy**
   - Uploads the built `.next` directory
   - Configures serverless functions
   - Sets up CDN and routing

## Environment Variables

Each app may need different environment variables:

### Web App (`apps/web`)
- `NEXT_PUBLIC_API_URL` - Backend API endpoint
- `NEXT_PUBLIC_LENS_API_URL` - Lens Protocol API
- `NEXT_PUBLIC_LIVEPEER_KEY` - Livepeer streaming key
- Other service keys...

### Embed App (`apps/embed`)
- `NEXT_PUBLIC_MAIN_APP_URL` - URL of main web app
- Service configuration...

### OG App (`apps/og`)
- `NEXT_PUBLIC_MAIN_APP_URL` - URL of main web app
- Image generation settings...

Add these in Vercel Dashboard → Project Settings → Environment Variables

## Monorepo Considerations

### Why Special Build Commands?

The build commands use `cd ../..` because:
1. Apps are in `apps/` subdirectory
2. Shared packages are in `packages/` 
3. Pnpm workspace needs root `pnpm-workspace.yaml`
4. Dependencies must be installed from root

### What Gets Deployed?

Only the specific app and its dependencies:
- The app's code (e.g., `apps/web/`)
- Shared packages it uses (e.g., `packages/ui/`)
- Built `.next` directory
- `node_modules` (automatically optimized by Vercel)

### What's Excluded?

See `.vercelignore`:
- Other apps (mobile, contracts, etc.)
- Development files
- Test files
- Documentation

## Performance Optimization

Vercel automatically provides:
- ✅ CDN distribution (Edge Network)
- ✅ Automatic HTTPS
- ✅ Image optimization
- ✅ Code splitting
- ✅ Serverless functions
- ✅ Preview deployments for PRs

## Continuous Deployment

Once connected:

```
GitHub Push → Vercel Build → Deploy → Live
     │              │           │        │
     │              │           │        └─> Production URL
     │              │           └─────> Preview URL (for PRs)
     │              └────> Build logs in dashboard
     └───────> Automatic trigger
```

Every push to main = new production deployment!  
Every PR = new preview deployment!

## Troubleshooting Builds

Common issues and solutions:

| Issue | Solution |
|-------|----------|
| "Module not found" | Ensure workspace dependencies are in root package.json |
| "Build failed" | Check build logs, verify all environment vars are set |
| "Out of memory" | May need Pro plan for large builds |
| "Command not found: pnpm" | Should auto-install, but check build command |

## Costs

Vercel Pricing:
- **Hobby (Free)**: Perfect for personal projects
  - 100GB bandwidth/month
  - Unlimited websites
  - Automatic HTTPS
  
- **Pro ($20/month)**: For production apps
  - 1TB bandwidth/month  
  - Team collaboration
  - Analytics included

Most developers start with the free tier! 🎉

## Next Steps

1. ✅ Deploy your first app (see [VERCEL_QUICKSTART.md](VERCEL_QUICKSTART.md))
2. ✅ Set up environment variables
3. ✅ Configure custom domain (optional)
4. ✅ Set up other apps if needed
5. ✅ Enable Vercel Analytics
6. ✅ Monitor your deployments

---

For detailed instructions, see [DEPLOYMENT.md](DEPLOYMENT.md)
