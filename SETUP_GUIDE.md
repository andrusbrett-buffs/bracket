# FADUNKADUNK Bracket - Deployment Guide

This guide will walk you through deploying your bracket online with Firebase (shared voting) and GitHub Pages (free hosting).

---

## Part 1: Set Up Firebase (Free Database)

### Step 1: Create a Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click **"Create a project"** (or "Add project")
3. Enter a project name: `fadunkadunk-bracket` (or similar)
4. Disable Google Analytics (optional, not needed)
5. Click **Create Project**

### Step 2: Create a Realtime Database

1. In your Firebase project, click **"Build"** in the left sidebar
2. Click **"Realtime Database"**
3. Click **"Create Database"**
4. Choose a location (pick the closest to your users)
5. Select **"Start in test mode"** (we'll secure it later)
6. Click **Enable**

### Step 3: Get Your Firebase Config

1. Click the **gear icon** ⚙️ next to "Project Overview"
2. Click **"Project settings"**
3. Scroll down to **"Your apps"**
4. Click the **web icon** `</>`
5. Register your app with a nickname (e.g., "fadunkadunk-web")
6. **DON'T** check "Firebase Hosting" (we're using GitHub Pages)
7. Click **"Register app"**
8. You'll see a config object like this:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSyB.....................",
  authDomain: "fadunkadunk-bracket.firebaseapp.com",
  databaseURL: "https://fadunkadunk-bracket-default-rtdb.firebaseio.com",
  projectId: "fadunkadunk-bracket",
  storageBucket: "fadunkadunk-bracket.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123..."
};
```

9. **Copy this entire config** - you'll need it next!

### Step 4: Update Your HTML Files

Open both `fadunkadunk_voting.html` and `fadunkadunk_results.html` and find this section near the top of the `<script>`:

```javascript
// ============================================
// FIREBASE CONFIGURATION
// Replace these values with your Firebase project config
// ============================================
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
    ...
};
```

**Replace the entire `firebaseConfig` object** with the one you copied from Firebase.

### Step 5: Set Database Rules (Security)

1. In Firebase Console, go to **Realtime Database**
2. Click the **"Rules"** tab
3. Replace the rules with:

```json
{
  "rules": {
    "votes": {
      ".read": true,
      ".write": true
    }
  }
}
```

4. Click **Publish**

> ⚠️ **Note:** These rules allow anyone to read/write. For a small league this is fine. For more security, you can add authentication later.

---

## Part 2: Deploy to GitHub Pages (Free Hosting)

### Step 1: Create a GitHub Account

1. Go to [github.com](https://github.com)
2. Sign up for a free account (if you don't have one)

### Step 2: Create a New Repository

1. Click the **+** icon in the top right
2. Click **"New repository"**
3. Name it: `fadunkadunk-bracket` (or any name you like)
4. Make it **Public** (required for free GitHub Pages)
5. Click **"Create repository"**

### Step 3: Upload Your Files

1. On your new repository page, click **"uploading an existing file"**
2. Drag and drop these 3 files:
   - `fadunkadunk_voting.html`
   - `fadunkadunk_results.html`
   - `fadunkadunk_interactive.html`
3. Add a commit message: "Initial upload"
4. Click **"Commit changes"**

### Step 4: Rename the Voting File (Important!)

GitHub Pages needs an `index.html` file. Let's rename your voting page:

1. Click on `fadunkadunk_voting.html`
2. Click the **pencil icon** ✏️ to edit
3. At the top, change the filename from `fadunkadunk_voting.html` to `index.html`
4. Click **"Commit changes"**

### Step 5: Enable GitHub Pages

1. Go to your repository's **Settings** (tab at the top)
2. Scroll down to **"Pages"** in the left sidebar
3. Under "Source", select **"Deploy from a branch"**
4. Under "Branch", select **"main"** and **"/ (root)"**
5. Click **Save**
6. Wait 1-2 minutes for deployment

### Step 6: Get Your Live URL

1. Refresh the Settings > Pages page
2. You'll see: **"Your site is live at https://YOUR_USERNAME.github.io/fadunkadunk-bracket/"**
3. That's your live URL! 🎉

---

## Your Files Are Now Live!

| Page | URL |
|------|-----|
| Voting | `https://YOUR_USERNAME.github.io/fadunkadunk-bracket/` |
| Results | `https://YOUR_USERNAME.github.io/fadunkadunk-bracket/fadunkadunk_results.html` |
| Browse | `https://YOUR_USERNAME.github.io/fadunkadunk-bracket/fadunkadunk_interactive.html` |

---

## Sharing with Your League

Send your league members this link to vote:
```
https://YOUR_USERNAME.github.io/fadunkadunk-bracket/
```

They can:
1. Click any destination to see details
2. Make picks for all 24 matchups
3. Enter their name and submit
4. View live results that update in real-time!

---

## Troubleshooting

### "Offline (Local Mode)" showing instead of "Connected"
- Double-check your Firebase config is correct
- Make sure you created a **Realtime Database** (not Firestore)
- Verify the `databaseURL` includes `-default-rtdb`

### Changes not showing on live site
- GitHub Pages can take 1-5 minutes to update
- Try a hard refresh: `Ctrl+Shift+R` (Windows) or `Cmd+Shift+R` (Mac)

### Firebase says "Permission Denied"
- Go to Firebase Console > Realtime Database > Rules
- Make sure the rules allow read/write as shown above

---

## Optional: Custom Domain

If you want a custom domain like `bracket.fadunkadunk.com`:

1. Buy a domain from Namecheap, Google Domains, etc.
2. In GitHub repo Settings > Pages, click "Add a custom domain"
3. Follow the DNS configuration instructions

---

## Need Help?

The files will work in "local mode" even without Firebase - votes just won't sync across devices. Firebase is only needed for the real-time shared experience.

Happy voting! 🏆
