# RajFrames Portfolio — Deployment Guide

A static portfolio site with a working EmailJS contact form. No backend server required.

---

## 📁 File Structure

```
rajframes-portfolio/
├── index.html       ← The entire site (frontend + EmailJS wired in)
├── vercel.json      ← Vercel static deployment config
└── README.md        ← This file
```

---

## ⚡ Step 1 — Set Up EmailJS (5 minutes)

### 1.1 Create an EmailJS account
Go to → https://www.emailjs.com/ and sign up (free tier: 200 emails/month).

### 1.2 Add an Email Service
1. Dashboard → **Email Services** → **Add New Service**
2. Choose **Gmail**
3. Sign in with `rajkaranchaudhary2009@gmail.com`
4. Give it a name like `rajframes_service`
5. Click **Connect Account** and authorize
6. Copy the **Service ID** (looks like `service_xxxxxxx`)

### 1.3 Create an Email Template
1. Dashboard → **Email Templates** → **Create New Template**
2. Set the template up like this:

**Subject:**
```
New Project Inquiry from {{from_name}} — {{project_type}}
```

**Body:**
```
Hi Raj,

You have a new project inquiry from your portfolio!

---
Name:         {{from_name}}
Email:        {{reply_to}}
Project Type: {{project_type}}
Budget:       {{budget}}
Deadline:     {{deadline}}

Message:
{{message}}
---

Reply directly to: {{reply_to}}
```

3. Set **To Email** → `rajkaranchaudhary2009@gmail.com`
4. Save and copy the **Template ID** (looks like `template_xxxxxxx`)

### 1.4 Get your Public Key
Dashboard → **Account** → **General** tab → Copy **Public Key**

---

## 🔧 Step 2 — Add Your Keys to index.html

Open `index.html` and find these 3 placeholders (use Ctrl+F):

| Placeholder | Replace with |
|---|---|
| `YOUR_EMAILJS_PUBLIC_KEY` | Your Public Key from step 1.4 |
| `YOUR_SERVICE_ID` | Service ID from step 1.2 |
| `YOUR_TEMPLATE_ID` | Template ID from step 1.3 |

Example (line ~9):
```js
emailjs.init({ publicKey: "abc123XYZ" });
```

Example (line ~1095):
```js
emailjs.send('service_abc123', 'template_xyz789', templateParams)
```

---

## 🐙 Step 3 — Push to GitHub

```bash
# In your terminal, navigate to this folder
cd rajframes-portfolio

# Initialize git
git init
git add .
git commit -m "Initial commit — RajFrames portfolio"

# Create a new repo on github.com named: rajframes-portfolio
# Then connect and push:
git remote add origin https://github.com/YOUR_GITHUB_USERNAME/rajframes-portfolio.git
git branch -M main
git push -u origin main
```

---

## 🚀 Step 4 — Deploy on Vercel

1. Go to → https://vercel.com/new
2. Click **Import Git Repository**
3. Select your `rajframes-portfolio` repo
4. Framework Preset: leave as **Other** (it auto-detects static)
5. Click **Deploy** — done in ~30 seconds

Your site will be live at:
`https://rajframes-portfolio.vercel.app`

### Custom Domain (optional)
Vercel Dashboard → your project → **Settings** → **Domains** → add your domain.

---

## 🔄 Future Updates

Any `git push` to `main` auto-triggers a Vercel redeploy. Just:
```bash
git add .
git commit -m "Update portfolio"
git push
```

---

## 🧪 Testing the Contact Form

Before going live, test by filling in the form on your local `index.html` (open it in a browser). Check `rajkaranchaudhary2009@gmail.com` inbox within ~30 seconds.

---

## 🛟 Troubleshooting

| Problem | Fix |
|---|---|
| Email not arriving | Check spam folder; verify Service ID and Template ID are correct |
| "Something went wrong" error | Open browser console (F12) and check the EmailJS error message |
| Vercel deploy fails | Make sure `vercel.json` is in the root folder alongside `index.html` |
| Gmail auth issues | Re-connect Gmail service in EmailJS dashboard |

---

Built with ❤️ — RajFrames 2025
