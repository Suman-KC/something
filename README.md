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

### **A. Here is your Server's Public IP/Hostname**
## 217.217.249.145 this will be useful for putting custom domain

You need to know how Vercel will connect to your MySQL database.


**📝 Write this down - you'll need it later!**

---

## 🔐 **Step 2: Generate NEXTAUTH_SECRET**

Run this command to generate a secure secret:

**Windows PowerShell:**
npx auth-secret
```

**📝 Copy this secret - you'll need it later!**

```

## 📤 **Step 3: Push Code to GitHub**


### **B. Create GitHub Repository**



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


✅ **Checkpoint:** Your code should now be visible at `https://github.com/YOUR_USERNAME/unity-ed-frontend`

---

## 🌐 **Step 4: Deploy to Vercel**

### **A. Sign Up for Vercel**

1. Go to **https://vercel.com/signup**
2. Click **"Continue with GitHub"**
3. Click **"Authorize Vercel"** when prompted
4. Complete any additional setup prompts

### **B. Import Your Project**

# 1. On Vercel dashboard, click **"Add New..."** → **"Project"**
# 2. In "Import Git Repository" section, find **`unity-ed`**
   - If you don't see it, click "Adjust GitHub App Permissions" → Grant access
# 3. Click **"Import"**

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
Value: mysql://unityed:%23%3F%5BtvG%23UPv0%7Dq8vV@147.93.153.72:3306/unityed_unity_ed_db
```
Click **"Add"**

#### **Variable 2: NEXTAUTH_URL**
```
Name:  NEXTAUTH_URL  
https://unity-ed.vercel.app   "here you have to write whatever is the vercel link for vercel app"


*(Tip: Leave this empty for now, Vercel will auto-fill it after first deploy, or use your project name)*
``` 
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
```
**Wait 2-3 minutes** while Vercel:
- Installs dependencies
- Runs Prisma generate
- Builds your Next.js app
- Deploys to their edge network

---
```




## ✅ **Step 6: Verify Deployment**

### **A. Check Deployment Status**

Back in Vercel:
- If deployment succeeds: You'll see **"Congratulations! Your project has been deployed"** 🎉
- If it fails: Click on the deployment to see **Build Logs** (see troubleshooting below)

### **B. Visit Your Live App**

1. Vercel will show you a URL like: `https://unity-ed-frontend-abc123.vercel.app`
2. Click **"Visit"** or open the URL
3. Your app is now LIVE! 🌍




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




## 🎨 **For Custom Domain **
```
Want to use your own domain instead of `xyz.vercel.app`?

1. In Vercel project → **Settings** → **Domains**
2. Enter your domain: `unity-ed.com`
3. Follow Vercel's DNS instructions
4. Update `NEXTAUTH_URL` environment variable to your custom domain

---
```



## 🆘 **Need Help?**

### **Vercel Logs**
- **Build Logs:** See what happened during deployment
- **Runtime Logs:** See live errors from your app
- **Access:** Project → Deployments → Click deployment → View Logs



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
DATABASE_URL="mysql://unityed:%23%3F%5BtvG%23UPv0%7Dq8vV@147.93.153.72:3306/unityed_unity_ed_db"
NEXTAUTH_URL="https://unityed.site"
NEXTAUTH_SECRET="hJeIY7lmRrD3Ad/3i3nVrAjfqAaIehfcjsLYc1IL0Nc="
NODE_ENV="production"

```

Save these securely!

 

## 🚀 **Next Steps (Optional)**

1. **Set up custom domain** (your own URL)
 Ready for production! ✅
