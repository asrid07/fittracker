# 💪 FitTracker AI — Asrid's Personal Fitness Dashboard

A fully private, secure fitness tracking app with:
- 🔐 Secure login via Supabase Auth
- 🔄 Data syncs across ALL devices
- 🤖 AI Personal Trainer (Coach Rex) via Claude API
- 📊 Full tracking: weight, meals, gym, water, supplements, photos
- 🌐 Hosted free on GitHub Pages

---

## 📁 File Structure

```
fittracker/
├── index.html      ← Login page
├── app.html        ← Main fitness app
├── supabase.js     ← Supabase config (YOU MUST EDIT THIS)
└── README.md       ← This file
```

---

## 🚀 Setup Guide

### STEP 1 — Supabase Setup

1. Go to **supabase.com** → Create free account
2. Click **New Project** → Name: `fittracker-asrid`
3. Select Region: **Southeast Asia (Singapore)**
4. Wait for project to initialize (~2 min)

#### Create Database Table
Go to **SQL Editor** → New Query → Run this:

```sql
create table fittracker_data (
  id uuid default gen_random_uuid() primary key,
  user_id uuid references auth.users(id) on delete cascade,
  data_key text not null,
  data_value jsonb,
  updated_at timestamp with time zone default now(),
  unique(user_id, data_key)
);

alter table fittracker_data enable row level security;

create policy "Users can only access their own data"
  on fittracker_data for all
  using (auth.uid() = user_id);
```

#### Create Your User Account
- Go to **Authentication** → **Users** → **Add user** → **Create new user**
- Email: your email (e.g. asrid@gmail.com)
- Password: your chosen password
- Click **Create user**

#### Get Your API Keys
- Go to **Settings** → **API**
- Copy **Project URL** (looks like https://xxxx.supabase.co)
- Copy **anon public** key (starts with eyJ...)

---

### STEP 2 — Update supabase.js

Open `supabase.js` and replace the placeholder values:

```javascript
const SUPABASE_URL = 'https://YOUR-PROJECT-ID.supabase.co';
const SUPABASE_ANON_KEY = 'eyJ...your-anon-key...';
```

---

### STEP 3 — GitHub Pages Deployment

1. Go to **github.com** → Create account (free)
2. Click **New repository** → Name: `fittracker`
3. Set to **Private** ✅ (keeps your code private)
4. Click **Create repository**
5. Upload all 4 files: `index.html`, `app.html`, `supabase.js`, `README.md`
6. Go to **Settings** → **Pages**
7. Source: **Deploy from branch** → **main** → **/ (root)**
8. Click **Save**
9. Wait 2-3 minutes → your app is live at:
   `https://YOUR-USERNAME.github.io/fittracker`

---

### STEP 4 — Open on Android

1. Open Chrome on your phone
2. Go to `https://YOUR-USERNAME.github.io/fittracker`
3. Login with your Supabase credentials
4. Tap **⋮ menu** → **Add to Home Screen**
5. ✅ Installed as PWA — works like a native app!

---

### STEP 5 — Add Claude API Key (Coach Rex)

1. Login to the app
2. Go to **⚙️ Settings** tab
3. Enter your Claude API key (sk-ant-...)
4. Click **Save API Key**
5. Coach Rex is now ACTIVE and synced across devices! 🔥

---

## 🔒 Privacy & Security

| Data | Where stored | Who can see |
|------|-------------|-------------|
| Your fitness data | Supabase database | Only you (Row Level Security) |
| Photos | Supabase storage | Only you (private bucket) |
| Password | Supabase Auth (hashed) | Nobody — encrypted |
| API key | Supabase database | Only you |
| HTML code | GitHub | Visible but contains no data |

---

## 📱 Features

- 🏠 **Home** — Weight progress, daily stats, water tracker, Coach Rex tip
- 🍽️ **Meals** — 7-meal checklist + food logger with macros
- 🏋️ **Gym** — Day-specific workouts, sets/reps guide, workout log
- 💧 **Water** — 9-cup tracker, timed schedule, history
- ⚖️ **Weight** — Log weight + body fat, chart, 8-week roadmap
- 💊 **Supps** — 8 supplement checklist with adherence history
- 📸 **Photos** — Take/upload progress photos, Before vs Now comparison
- 🤖 **Coach Rex** — AI personal trainer, 8 quick commands, full chat
- 📊 **Progress** — Weekly stats, streaks, blood report action plan
- ⚙️ **Settings** — API key, data export, account management

---

## 🩸 Blood Report Flags (Pre-configured)

- 🔴 Vitamin D: 12.4 ng/mL — DEFICIENT
- 🔴 HDL: 36 mg/dL — LOW
- 🟡 Uric Acid: 7.5 — BORDERLINE
- 🟡 BUN/Creatinine: 22.8 — ELEVATED
- 🟡 B12: 329 pg/mL — LOW-NORMAL

---

*Built for Asrid Cheerngodan — Personal Fitness Dashboard*
