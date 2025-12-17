# 🚀 Unity-Ed - Complete Vercel Deployment Guide

## ⏱️ Estimated Time: 15-20 minutes
## 💰 Cost: $0 (Free tier)

---

## 📋 **What You'll Need**

- [x] This project on your local machine
- [ ] GitHub account (free) - https://github.com/signup
- [ ] Vercel account (free) - https://vercel.com/signup
- [ ] Your cPanel/MySQL database credentials

---

## 🎯 **Step 1: Prepare Your Database Connection String**

### **A. Find Your Server's Public IP/Hostname**

You need to know how Vercel will connect to your MySQL database.

**Option 1: Via cPanel (easiest)**
1. Log into cPanel
2. Look at the URL - it usually contains your server hostname
   - Example: `cpanel.yourserver.com` or `server123.yourhost.com`

**Option 2: Via Terminal/SSH**
```bash
# SSH into your cPanel server
ssh unityed@your-server.com

# Get public IP
curl ifconfig.me
```

### **B. Prepare Your DATABASE_URL**

Format:
```
mysql://USERNAME:PASSWORD@HOSTNAME:PORT/DATABASE_NAME
```

Your actual values (update HOSTNAME):
```
mysql://unityed_root:o4.Q-kZifAXLi.O@YOUR_SERVER_HOSTNAME_OR_IP:3306/unityed_unity_ed
```

**Examples:**
- With IP: `mysql://unityed_root:o4.Q-kZifAXLi.O@123.45.67.89:3306/unityed_unity_ed`
- With hostname: `mysql://unityed_root:o4.Q-kZifAXLi.O@server.yourhost.com:3306/unityed_unity_ed`

**📝 Write this down - you'll need it later!**

---

## 🔐 **Step 2: Generate NEXTAUTH_SECRET**

Run this command to generate a secure secret:

**Windows PowerShell:**
```powershell
-join ((48..57) + (65..90) + (97..122) | Get-Random -Count 32 | ForEach-Object {[char]$_})
```

**Mac/Linux Terminal:**
```bash
openssl rand -base64 32
```

**📝 Copy this secret - you'll need it later!**

---

## 📤 **Step 3: Push Code to GitHub**

### **A. Initialize Git Repository**

Open PowerShell/Terminal in your project folder:

```bash
# Navigate to project
cd d:\Costumer-project\Nextjs\unity-ed-frontend\unity-ed

# Initialize Git
git init

# Add all files
git add .

# Create initial commit
git commit -m "Initial commit - Unity-Ed application"
```

### **B. Create GitHub Repository**

1. Go to **https://github.com/new**
2. Fill in:
   - **Repository name:** `unity-ed-frontend`
   - **Description:** (optional) "Unity Ed - Gamified Learning Platform"
   - **Visibility:** Choose **Private** (recommended)
   - **IMPORTANT:** Do NOT check any boxes (no README, no .gitignore, no license)
3. Click **"Create repository"**

### **C. Push Your Code to GitHub**

GitHub will show you commands. Copy them, but here's the general format:

```bash
# Add GitHub as remote (replace YOUR_USERNAME)
git remote add origin https://github.com/YOUR_USERNAME/unity-ed-frontend.git

# Rename branch to main
git branch -M main

# Push to GitHub
git push -u origin main
```

**If you need to authenticate:**
- Username: Your GitHub username
- Password: Create a **Personal Access Token**
  - Go to: https://github.com/settings/tokens
  - Click "Generate new token (classic)"
  - Name it: "Vercel Deployment"
  - Check: `repo` (full control of private repositories)
  - Click "Generate token"
  - **Copy the token** (you can't see it again!)
  - Use this token as your password

✅ **Checkpoint:** Your code should now be visible at `https://github.com/YOUR_USERNAME/unity-ed-frontend`

---

## 🌐 **Step 4: Deploy to Vercel**

### **A. Sign Up for Vercel**

1. Go to **https://vercel.com/signup**
2. Click **"Continue with GitHub"**
3. Click **"Authorize Vercel"** when prompted
4. Complete any additional setup prompts

### **B. Import Your Project**

1. On Vercel dashboard, click **"Add New..."** → **"Project"**
2. In "Import Git Repository" section, find **`unity-ed-frontend`**
   - If you don't see it, click "Adjust GitHub App Permissions" → Grant access
3. Click **"Import"**

### **C. Configure Build Settings**

Vercel will auto-detect Next.js settings:

- **Framework Preset:** Next.js ✅
- **Root Directory:** `./` (leave as is)
- **Build Command:** (leave default) ✅
- **Output Directory:** `.next` ✅
- **Install Command:** (leave default) ✅

**DO NOT CLICK DEPLOY YET!** ⚠️

### **D. Add Environment Variables**

**IMPORTANT:** Scroll down to **"Environment Variables"** section

Add these variables **one by one**:

#### **Variable 1: DATABASE_URL**
```
Name:  DATABASE_URL
Value: mysql://unityed_root:o4.Q-kZifAXLi.O@YOUR_SERVER_IP_OR_HOSTNAME:3306/unityed_unity_ed
```
*(Use the value you prepared in Step 1)*

Click **"Add"**

#### **Variable 2: NEXTAUTH_URL**
```
Name:  NEXTAUTH_URL  
Value: https://unity-ed-frontend-YOUR_VERCEL_PROJECT.vercel.app
```
*(Note: You can update this later to your custom domain)*

*(Tip: Leave this empty for now, Vercel will auto-fill it after first deploy, or use your project name)*

Click **"Add"**

#### **Variable 3: NEXTAUTH_SECRET**
```
Name:  NEXTAUTH_SECRET
Value: (paste the secret you generated in Step 2)
```

Click **"Add"**

#### **Variable 4: NODE_ENV**
```
Name:  NODE_ENV
Value: production
```

Click **"Add"**

### **E. Deploy!**

Now click **"Deploy"** 🚀

**Wait 2-3 minutes** while Vercel:
- Installs dependencies
- Runs Prisma generate
- Builds your Next.js app
- Deploys to their edge network

---

## 🔌 **Step 5: Configure Database Remote Access**

While Vercel is deploying, configure your cPanel MySQL to accept remote connections:

### **In cPanel:**

1. Search for **"Remote MySQL®"** in cPanel
2. Under "Add Access Host", enter: `%.vercel-dns.com`
   - This allows all Vercel servers to connect
   - Alternative (less secure): Use `%` to allow from anywhere
3. Click **"Add Host"**

✅ **Checkpoint:** You should see the host in "Access Hosts" list

---

## ✅ **Step 6: Verify Deployment**

### **A. Check Deployment Status**

Back in Vercel:
- If deployment succeeds: You'll see **"Congratulations! Your project has been deployed"** 🎉
- If it fails: Click on the deployment to see **Build Logs** (see troubleshooting below)

### **B. Visit Your Live App**

1. Vercel will show you a URL like: `https://unity-ed-frontend-abc123.vercel.app`
2. Click **"Visit"** or open the URL
3. Your app is now LIVE! 🌍

### **C. Test Core Functionality**

1. **Homepage loads** ✅
2. **Login page** (`/login`) ✅
3. **Try logging in** with your credentials
4. **Check dashboards:**
   - Admin: `/dashboard/admin`
   - Teacher: `/dashboard/teacher`
   - Student: `/dashboard/student`

---

## 🐛 **Troubleshooting**

### **Issue 1: Build Failed**

**Check Build Logs:**
1. Click on the failed deployment
2. Read the error message

**Common fixes:**
- **Prisma error:** Make sure `binaryTargets = ["native", "debian-openssl-1.1.x"]` is in `prisma/schema.prisma`
- **TypeScript error:** Fix the error locally, commit, push again
- **Environment variable missing:** Add it in Vercel Project Settings → Environment Variables

### **Issue 2: Database Connection Failed**

**Error:** "Can't reach database server" or ECONNREFUSED

**Fixes:**
1. **Check Remote MySQL:** Make sure `%.vercel-dns.com` is added in cPanel
2. **Verify DATABASE_URL:**
   - Go to Vercel Project Settings → Environment Variables
   - Check DATABASE_URL is correct (username, password, hostname, port, database name)
3. **Test connection manually:**
   ```bash
   # From your local machine
   mysql -h YOUR_SERVER_IP -u unityed_root -p
   # Enter password: o4.Q-kZifAXLi.O
   ```
4. **Check MySQL port:** Most servers use port 3306, but some use custom ports

### **Issue 3: NextAuth Error**

**Error:** "NEXTAUTH_URL is not configured"

**Fix:**
1. Go to Vercel Project Settings → Environment Variables
2. Update `NEXTAUTH_URL` to your actual Vercel app URL
3. Redeploy: Deployments → Three dots (···) → Redeploy

### **Issue 4: 500 Internal Server Error**

**Check Runtime Logs:**
1. In Vercel dashboard → Your project → **"Logs"**
2. Look for errors when you try to access the page

**Common fixes:**
- **Database connection:** See Issue 2
- **Missing environment variable:** Add it in Project Settings
- **API route error:** Check the specific API route logs

---

## 🔄 **How to Update Your App**

After deployment, whenever you make changes:

```bash
# Make your code changes
# ...

# Commit changes
git add .
git commit -m "Description of changes"

# Push to GitHub
git push
```

**Vercel will automatically:**
- Detect the push
- Build your app
- Deploy the new version
- All in ~2 minutes! 🚀

---

## 🎨 **Custom Domain (Optional)**

Want to use your own domain instead of `xyz.vercel.app`?

1. In Vercel project → **Settings** → **Domains**
2. Enter your domain: `unity-ed.com`
3. Follow Vercel's DNS instructions
4. Update `NEXTAUTH_URL` environment variable to your custom domain

---

## 📊 **What You Get with Vercel (Free Tier)**

✅ **Generous limits:**
- 100 GB bandwidth per month
- Unlimited deployments
- Automatic HTTPS
- Global CDN (fast worldwide)
- Preview deployments (for pull requests)

✅ **No maintenance:**
- Automatic Node.js version management
- Zero-downtime deployments
- Built-in monitoring

✅ **Perfect for Prisma:**
- No memory issues
- Correct binary targets automatically downloaded
- Optimized for Next.js

---

## 🆘 **Need Help?**

### **Vercel Logs**
- **Build Logs:** See what happened during deployment
- **Runtime Logs:** See live errors from your app
- **Access:** Project → Deployments → Click deployment → View Logs

### **Database Connection Test**

Add this API route to test database connection:

Create `app/api/test-db/route.ts`:
```typescript
import { NextResponse } from 'next/server';
import { PrismaClient } from '@prisma/client';

const prisma = new PrismaClient();

export async function GET() {
  try {
    await prisma.$connect();
    const userCount = await prisma.user.count();
    return NextResponse.json({ 
      success: true, 
      message: 'Database connected!',
      userCount 
    });
  } catch (error: any) {
    return NextResponse.json({ 
      success: false, 
      error: error.message 
    }, { status: 500 });
  }
}
```

Visit: `https://your-app.vercel.app/api/test-db`

---

## ✅ **Deployment Checklist**

- [ ] Step 1: Database URL prepared
- [ ] Step 2: NEXTAUTH_SECRET generated
- [ ] Step 3: Code pushed to GitHub
- [ ] Step 4: Deployed to Vercel
- [ ] Step 5: Remote MySQL configured
- [ ] Step 6: App tested and working

---

## 🎉 **You're Done!**

Your Unity-Ed app is now live and accessible from anywhere in the world!

**Your URLs:**
- Production: `https://your-project.vercel.app`
- Admin Dashboard: `https://your-project.vercel.app/dashboard/admin`
- Teacher Dashboard: `https://your-project.vercel.app/dashboard/teacher`
- Student Dashboard: `https://your-project.vercel.app/dashboard/student`

**Database:** Still on your cPanel (no migration needed!)

---

## 📝 **Environment Variables Reference**

For your records, here are all the environment variables used:

```env
DATABASE_URL=mysql://unityed_root:o4.Q-kZifAXLi.O@YOUR_SERVER:3306/unityed_unity_ed
NEXTAUTH_URL=https://your-app.vercel.app
NEXTAUTH_SECRET=your-generated-secret
NODE_ENV=production
```

Save these securely!

---

## 🚀 **Next Steps (Optional)**

1. **Set up custom domain** (your own URL)
2. **Configure email** (for password resets, notifications)
3. **Set up monitoring** (Vercel Analytics)
4. **Enable preview deployments** (test changes before going live)
5. **Add team members** (collaborate on Vercel)

---

**Need help?** Open an issue or check Vercel's documentation at https://vercel.com/docs

**Deployment Date:** $(Get-Date -Format "yyyy-MM-dd HH:mm")
**Status:** Ready for production! ✅
