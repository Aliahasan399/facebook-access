<div align="center">
  
# 🚀 Facebook Access — Hermes Agent Skill

**Automate Facebook Pages, Groups, Posts, Comments & Messages**  
*via Meta Graph API*

[![GitHub](https://img.shields.io/badge/Made%20for-Hermes%20Agent-6C47FF)](https://hermes-agent.nousresearch.com)
[![License](https://img.shields.io/badge/license-MIT-blue)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen)](https://github.com/Aliahasan399/facebook-access/pulls)

</div>

---

## 📖 What Is This?

This is a **skill for Hermes Agent** — an AI assistant framework — that gives it the power to **control your Facebook Pages and Groups** automatically.

With this skill, you can tell your AI assistant things like:

- *"Post this message on my Facebook page"*
- *"Show me my latest posts and how many likes they got"*
- *"Reply to that comment"*
- *"Check my page inbox messages"*
- *"Post this in my Facebook group"*

And it just works. No manual logging in. No copy-pasting. All from your terminal or Telegram.

---

## ✨ What Can It Do?

| Feature | Description |
|---|---|
| 📋 **List Pages** | See all Facebook Pages you manage |
| 📝 **Create Posts** | Post text updates to your page |
| 📊 **Engagement Stats** | See likes, comments, shares on your posts |
| 💬 **Reply to Comments** | Reply to any comment on your posts |
| 📨 **Page Inbox** | Read and reply to messages |
| 👥 **List Groups** | See groups you're part of |
| 📢 **Group Posts** | Post to groups you belong to |
| 👤 **Group Members** | See who's in your groups |

---

## 🔧 What You Need to Set Up

Before it works, you need **one thing**: a **Facebook Access Token**.

This is like a key that lets the script talk to Facebook on your behalf. You get it from Meta's developer site. Don't worry — I'll walk you through every step.

---

## 🪜 Step-by-Step Setup Guide

### 🚀 One-Click Setup (Recommended)

If you already have Hermes Agent installed, just run:

```bash
# Clone the repo
git clone git@github.com:Aliahasan399/facebook-access.git
cd facebook-access

# Run one-click setup
python3 setup.py
```

The script will:
1. ✅ Detect your Hermes profile automatically
2. ✅ Copy skill files to the right location
3. ✅ Guide you through Facebook Access Token setup
4. ✅ Verify everything works

### 🛠️ Manual Setup

If you prefer to do it yourself, follow the steps below.

### Step 1: Create a Facebook App

1. Go to **[Meta Developer Portal](https://developers.facebook.com/apps/creation/)**
2. You'll see a list of **"Use Cases"** (each with a checkbox). Select:
   
   ✅ **"Manage everything on your Page"**  — *(has a 🚩 flag icon)*
   
   *Description: "Publish content and videos, moderate posts and comments from followers on your Page and get insights on engagement."*

3. Click **"Next"** (blue button, bottom-right)
4. Give your app a **name** (anything, e.g. "My Page Manager")
5. Enter your **email address**
6. Click **"Create App"**

![Quick tip] If you don't see the use case list, use this direct link:  
👉 [https://developers.facebook.com/apps/creation/](https://developers.facebook.com/apps/creation/)

### Step 2: Add the Pages API

1. From your app's **Dashboard**, look at the **left sidebar**
2. Scroll down and click **"Add Product"**
3. Find **"Pages API"** in the list and click **"Set Up"** next to it
4. That's it — Pages API is now added

🛑 *Don't select any other products like Marketing API, Threads API, etc.*

### Step 3: Get Your Access Token

1. Go to **Graph API Explorer**:  
   👉 [https://developers.facebook.com/tools/explorer/](https://developers.facebook.com/tools/explorer/)
2. From the dropdown at the top-right, select **your app** (the one you just created)
3. Click **"User Token"** → **"Get User Access Token"**
4. A popup will show with permission checkboxes. **Select ALL of these**:

```
☑ pages_show_list
☑ pages_manage_posts
☑ pages_read_engagement
☑ pages_manage_comments
☑ pages_manage_metadata
☑ pages_read_user_content
☑ pages_manage_engagement
☑ pages_messaging
☑ publish_to_groups
☑ groups_access_member_info
```

5. Click **"Generate"** — a long token string will appear
6. **Important:** Below the token, click the **"Exchange"** button (a blue link).  
   This turns your short-lived token into a **60-day token**.

📋 **Copy this token somewhere safe.** You'll need it in the next step.

### Step 4: Also Get a Page Token (for posting)

The token above lets you *see* things. To **post** on a page, you need a **Page Access Token**.

1. In the same Graph API Explorer, replace the URL with:
   ```
   GET /me/accounts
   ```
2. Click **Submit**. You'll see a list of your pages
3. Find your page in the list — each page has an `access_token` field
4. Copy that token. This is your **Page Access Token**

🎯 **Two tokens summary:**
| Token | What it's for |
|---|---|
| **User Token** (from Step 3) | Lists pages, groups — identifies *you* |
| **Page Token** (from Step 4) | Posts, comments, messages — acts as *your page* |

### Step 5: Switch Your App to Live Mode

Facebook apps start in **Development** mode. You need to switch to **Live** mode for the tokens to work.

1. Go to your app Dashboard: [https://developers.facebook.com/apps/](https://developers.facebook.com/apps/)
2. Click your app
3. In left sidebar, go to **Settings → Basic**
4. Fill in:
   - **Privacy Policy URL** — Use one of the templates in the `templates/` folder hosted on GitHub Pages or any free hosting
   - **Terms of Service URL** — Same as above
5. Scroll down to **App Mode** — it shows **"Development"**
6. Click the toggle to switch to **"Live"**
7. Click **"Save Changes"** at the bottom
8. 🔄 **Regenerate a fresh token** from Graph API Explorer (old tokens won't work after switching mode)

### Step 6: Add the Token to Your System

```bash
# Open your environment file
nano ~/.hermes/profiles/mybot/.env

# Add this line (replace with your actual token):
export FACEBOOK_ACCESS_TOKEN='your_token_here'

# Save and exit (Ctrl+X, then Y, then Enter)
```

> ⚠️ **Important:** Use **single quotes** `'...'` around the token! Facebook tokens can contain special characters (`$`, `` ` ``, `\`) that break things in double quotes.

### Step 7: Test If It Works

```bash
cd facebook-access/
python3 facebook_graph.py token-check
```

If you see your **App ID**, **User ID**, and a list of granted permissions — congratulations, you're set! 🎉

If it shows **"Pages: 0"**:
- Make sure you're logged into the **correct Facebook account** (the one that owns the page)
- Try generating the token again while logged into that account

---

## 🎮 How to Use

### List your pages
```bash
python3 facebook_graph.py list-pages
```

### Create a post
```bash
python3 facebook_graph.py create-post YOUR_PAGE_ID "Hello world! This is my first automated post."
```

### See recent posts & engagement
```bash
python3 facebook_graph.py get-engagement YOUR_PAGE_ID
```

### Reply to a comment
```bash
python3 facebook_graph.py reply-comment COMMENT_ID "Thanks for your feedback!"
```

### Check page inbox messages
```bash
python3 facebook_graph.py list-conversations YOUR_PAGE_ID
```

### List your groups
```bash
python3 facebook_graph.py list-groups
```

### Post to a group
```bash
python3 facebook_graph.py group-post GROUP_ID "Check out this cool thing!"
```

---

## 🐛 Common Problems & Fixes

| Problem | Reason | Solution |
|---|---|---|
| `(#200) Requires pages_manage_posts permission` | Token missing permissions | Regenerate token with ALL permissions checked |
| Token shows 0 pages | Wrong Facebook account | Generate token while logged into correct account |
| `Invalid JSON for postcard` | App still in Development mode | Switch to Live mode (Step 5) |
| Token works for 1 hour then stops | Didn't exchange for long-lived token | Click "Exchange" in Graph API Explorer |
| Shell shows weird characters with token | Special chars in token | Use single quotes `'token'` around it |
| `(#190) Your app is not whitelisted` | Need App Review | For personal use, keep app in Development mode |

---

## 📁 Repository Structure

```
facebook-access/
├── README.md                  ← You're reading it!
├── SKILL.md                   ← Hermes Agent skill definition
├── facebook_graph.py          ← Main script (all API magic)
├── scripts/
│   └── facebook_graph.py      ← Same script (for Hermes skill path)
├── templates/
│   ├── privacy-policy.html     ← For your Facebook app's Privacy Policy URL
│   ├── terms-of-service.html   ← For your Facebook app's ToS URL
│   └── data-deletion.html      ← Data deletion instructions
└── .gitignore
```

---

## 👨‍💻 Author

**Ali Ahsan** — *Created the original Hermes Agent facebook-access skill*

[![GitHub](https://img.shields.io/badge/GitHub-Aliahasan399-181717?style=flat&logo=github)](https://github.com/Aliahasan399)

---

## 📄 License

This project is open source under the **MIT License** — feel free to use, modify, and share.

---

<div align="center">
⭐ **If you find this useful, give it a star!** ⭐  
*Helps others discover it too.*
</div>
