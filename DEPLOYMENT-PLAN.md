# Big Wave Training - Deployment & Registration Plan

## Overview
Deploy the website and create a registration system with:
- 10-person limit per course date
- Email notifications to mikegeorge@gmail.com
- Database tracking registrations

---

## Part 1: Quick Fixes

### 1.1 Update Email
- [ ] Change contact email from mike@bigwavetraining.com to mikegeorge@gmail.com

---

## Part 2: Deployment Options

### Option A: GitHub Pages (Recommended - Free & Simple)
**Pros:** Free, automatic deploys from git, custom domain support
**Cons:** Static only (but we'll use n8n for backend)

Steps:
1. Create GitHub repo for the website
2. Push code to GitHub
3. Enable GitHub Pages in repo settings
4. Point bigwavetraining.com to GitHub Pages via Squarespace DNS

### Option B: Netlify (Also Good)
**Pros:** Free, drag & drop deploy, form handling built-in, custom domain
**Cons:** Form handling has limits on free tier

Steps:
1. Create Netlify account
2. Drag & drop website folder or connect to GitHub
3. Configure custom domain

### Option C: Vercel
Similar to Netlify, also free and easy.

### NOT Recommended: ngrok
- Only for temporary testing, not production
- URL changes each time
- Not suitable for a live site

**Recommendation:** GitHub Pages (you already have git set up)

---

## Part 3: Registration System with n8n

Since you already have n8n running, we'll use it for the backend:

### 3.1 Database: Google Sheets
Simple, visual, easy to manage. Columns:
- Timestamp
- Name
- Email
- Course Date
- Status (confirmed/waitlist)

### 3.2 n8n Workflow: "Big Wave Registration"

```
Form Submit (Webhook)
    ↓
Get Sheet Data (count registrations for selected date)
    ↓
If count < 10 → Add to Sheet + Send Confirmation Email
If count >= 10 → Add to Waitlist + Send Waitlist Email
    ↓
Send Notification to mikegeorge@gmail.com
```

### 3.3 Update Website Form
- Change form action to n8n webhook URL
- Add hidden field for tracking

---

## Part 4: Implementation Steps

### Phase 1: Quick Updates (5 min)
1. [ ] Update email to mikegeorge@gmail.com
2. [ ] Commit changes

### Phase 2: Create Registration Backend (30 min)
1. [ ] Create Google Sheet "Big Wave Registrations"
2. [ ] Create n8n workflow with webhook trigger
3. [ ] Add logic to count registrations per date
4. [ ] Add email notifications (confirmation + notification to Mike)
5. [ ] Test the workflow

### Phase 3: Connect Website to n8n (10 min)
1. [ ] Update form action to n8n webhook URL
2. [ ] Test form submission
3. [ ] Verify emails arrive

### Phase 4: Deploy to GitHub Pages (15 min)
1. [ ] Create GitHub repository
2. [ ] Push website code
3. [ ] Enable GitHub Pages
4. [ ] Test with github.io URL

### Phase 5: Connect Custom Domain (15 min)
1. [ ] In Squarespace DNS, add CNAME record pointing to GitHub Pages
2. [ ] Configure custom domain in GitHub repo settings
3. [ ] Wait for DNS propagation (can take up to 48 hours, usually faster)
4. [ ] Test bigwavetraining.com

---

## Email Templates

### Confirmation Email (to registrant)
Subject: You're In! Big Wave Training - [DATE]

### Waitlist Email (if over 10)
Subject: You're on the Waitlist - Big Wave Training

### Notification Email (to Mike)
Subject: New Registration: [NAME] for [DATE] ([COUNT]/10)

---

## Questions to Confirm

1. Do you have a GitHub account? If not, we'll create one.
2. Do you have access to Squarespace DNS settings for bigwavetraining.com?
3. For Google Sheets - should I use your mikegeorge@gmail.com Google account?
