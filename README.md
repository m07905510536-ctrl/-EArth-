# EArth – Premium Accessories PWA

A complete, installable Progressive Web App for the **EArth** accessories brand.
Built with React + Vite + Tailwind CSS + Supabase.

---

## 🚀 Quick Start

```bash
# 1. Install dependencies
npm install

# 2. Configure environment (optional for demo)
cp .env.example .env
# Fill in your Supabase URL and anon key

# 3. Start dev server
npm run dev

# 4. Open in Chrome → browser will prompt to install
```

---

## 📁 Project Structure

```
earth-pwa/
├── public/
│   └── icons/
│       ├── icon-192.png       # PWA icon (192×192)
│       └── icon-512.png       # PWA icon (512×512)
├── src/
│   ├── components/
│   │   ├── Navbar.jsx         # Sticky nav with PWA install button
│   │   ├── ProductCard.jsx    # Public product display card
│   │   └── ProductForm.jsx    # Add/edit product modal
│   ├── context/
│   │   ├── AuthContext.jsx    # Auth state (Supabase or demo)
│   │   └── ProductsContext.jsx# Products CRUD state
│   ├── hooks/
│   │   └── usePWAInstall.js   # beforeinstallprompt handler
│   ├── lib/
│   │   ├── supabase.js        # Supabase client
│   │   └── mockData.js        # Demo product data
│   ├── pages/
│   │   ├── PublicPage.jsx     # Landing + gallery + footer
│   │   ├── LoginPage.jsx      # Admin login
│   │   └── AdminDashboard.jsx # Product management
│   ├── App.jsx                # Root with provider setup
│   ├── main.jsx               # Entry point
│   └── index.css              # Global styles + Tailwind
├── index.html
├── vite.config.js             # Vite + VitePWA plugin
├── tailwind.config.js
└── .env.example
```

---

## 🔧 Supabase Setup

1. Create a project at [supabase.com](https://supabase.com)
2. Run this SQL in your **SQL Editor**:

```sql
CREATE TABLE products (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  title TEXT NOT NULL,
  description TEXT,
  price NUMERIC(10,2) NOT NULL,
  image_url TEXT,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

ALTER TABLE products ENABLE ROW LEVEL SECURITY;

-- Allow public read
CREATE POLICY "Public read" ON products FOR SELECT USING (true);

-- Allow authenticated write
CREATE POLICY "Auth write" ON products
  FOR ALL USING (auth.role() = 'authenticated');
```

3. Go to **Authentication → Users** and create your admin user
4. Copy your **Project URL** and **anon key** to `.env`

---

## 🎯 Demo Mode (No Supabase Required)

Without Supabase configured, the app runs in **demo mode**:
- 6 sample products shown
- Admin login: `admin@earth.com` / `earth2024`
- All CRUD operations work in-memory

---

## 📱 PWA Installation

The app will automatically prompt Chrome users to install when:
1. Served over HTTPS (or localhost)
2. Has a valid `manifest.webmanifest` ✓
3. Has a registered service worker ✓
4. Has 192×192 and 512×512 icons ✓

---

## 🎨 Design System

| Token | Value |
|-------|-------|
| Brand Red | `#E50000` |
| Black | `#000000` |
| Card BG | `#111111` |
| Surface | `#1A1A1A` |
| White | `#FFFFFF` |
| Display font | Bebas Neue |
| Body font | Inter |

---

## 📧 Support

**earthbrand11@gmail.com**
