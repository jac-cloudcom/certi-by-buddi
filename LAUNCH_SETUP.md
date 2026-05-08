# CERTI Landing Page — Launch Setup Guide

Your production-ready landing page is configured and ready to deploy. Follow these steps to go live.

---

## 📋 Pre-Launch Checklist

- [ ] Update your domain name in `og:url` meta tag (line 21)
- [ ] Set up Google Analytics ID and replace `G-XXXXXXXXXX` with your actual ID
- [ ] Set up Formspree form endpoint or alternative form service
- [ ] Test the form submission on staging
- [ ] Update footer contact email (currently placeholder)
- [ ] Test all links and navigation
- [ ] Mobile preview on actual devices
- [ ] Lighthouse audit for performance/SEO

---

## 🚀 Deployment Options

### Option 1: Vercel (Recommended)

1. **Push to GitHub**
   ```bash
   git init
   git add certi-landing-launch.html vercel.json
   git commit -m "Initial CERTI landing"
   git push origin main
   ```

2. **Create Vercel Project**
   - Go to [vercel.com](https://vercel.com)
   - Click "New Project"
   - Import your GitHub repo
   - Vercel auto-deploys on every push
   - Set environment variables in Settings → Environment Variables

3. **Point Custom Domain**
   - In Vercel settings, go to Domains
   - Add `certi.buddi.app` (or your domain)
   - Update your domain DNS to point to Vercel

4. **Set Environment Variables**
   - Go to Settings → Environment Variables
   - Add `GA_ID` = your Google Analytics ID

**Deploy time:** Instant (seconds)  
**Cost:** Free tier includes 1 project

---

### Option 2: Netlify

1. **Connect GitHub**
   - Go to [netlify.com](https://netlify.com)
   - Click "New site from Git"
   - Authorize GitHub and select your repo

2. **Basic Build Settings**
   - Leave "Build command" empty (static file)
   - Leave "Publish directory" blank (root)
   - Save

3. **Update Domain**
   - In Site Settings → Domain Management
   - Add your custom domain
   - Update DNS records

**Deploy time:** Instant  
**Cost:** Free

---

### Option 3: Your Own Hosting

If deploying to Apache, Nginx, or traditional hosting:

1. Upload `certi-landing-launch.html` to your web server
2. Set appropriate cache headers (see below)
3. Enable HTTPS (required)
4. Update canonical URL in meta tags

**Cache Headers (Nginx example):**
```nginx
# Static assets (7-day cache)
location ~* \.(js|css|png|jpg|jpeg|gif|svg|ico|woff2)$ {
  expires 7d;
  add_header Cache-Control "public, max-age=604800, immutable";
}

# HTML (no cache, always fresh)
location ~* \.html$ {
  expires off;
  add_header Cache-Control "public, max-age=0, must-revalidate";
}
```

---

## 🔧 Configuration Changes Required

### 1. Google Analytics Setup

1. Create a Google Analytics 4 account at [analytics.google.com](https://analytics.google.com)
2. Create a new property for CERTI
3. Copy your **Measurement ID** (starts with `G-`)
4. Replace `G-XXXXXXXXXX` on **line 37** with your ID

Current code:
```html
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
```

Should become:
```html
<script async src="https://www.googletagmanager.com/gtag/js?id=G-ABC123XYZ"></script>
```

And update line 40:
```javascript
gtag('config', 'G-ABC123XYZ');
```

### 2. Form Submission Setup

The form is currently configured to use **Formspree** (free service, no backend needed).

**Option A: Use Formspree (Easiest)**
1. Go to [formspree.io](https://formspree.io)
2. Sign up with email
3. Create new form for "CERTI Pilot"
4. Get your form endpoint: `https://formspree.io/f/XXXXXXXXXX`
5. Update line 486 in the HTML:
   ```html
   <form id="pilot-form" method="POST" action="https://formspree.io/f/YOUR_FORM_ID">
   ```

**Option B: Use Basin** (Alternative)
1. Go to [usebasin.com](https://usebasin.com)
2. Sign up and create new form
3. Get your endpoint and update the form action

**Option C: Netlify Forms** (If using Netlify)
- Netlify has built-in forms. Add `netlify` attribute:
  ```html
  <form id="pilot-form" method="POST" netlify>
  ```

### 3. Update Domain References

Search and replace these placeholders:
- `https://certi.buddi.app` → Your actual domain
- `hello@buddi.example` → Real contact email

Lines to update:
- Line 21: `og:url` meta tag
- Line 1261: Email href in CTA (if using direct email)
- Line 1288: Footer disclaimer

### 4. Update Footer Links

Line 1286-1290 — Update placeholder links to real pages:
```html
<a href="#">Verification</a>
<a href="#">Scan Analytics</a>
<a href="#">Rewards</a>
<a href="#">Brand Dashboard</a>
```

---

## 📊 Analytics Events Tracked

The page automatically tracks:

| Event | Trigger | Purpose |
|---|---|---|
| `cta_click` | Click on primary buttons | Count engagement |
| `pilot_signup` | Form submission | Track conversions |
| `page_view` | Page load | Google Analytics default |

You'll see these in Google Analytics → Events.

---

## 🔒 Security Checklist

- [x] HTTPS only (Vercel/Netlify auto-enable)
- [x] No sensitive data in HTML
- [x] Form submissions use secure service (Formspree encrypted)
- [x] X-Frame-Options header set
- [x] X-Content-Type-Options header set
- [ ] Add CSP header (optional, recommended):
  ```
  Content-Security-Policy: default-src 'self'; script-src 'self' https://www.googletagmanager.com; connect-src 'self' https://formspree.io
  ```

---

## 🎯 SEO Optimization Already Included

✅ Meta description optimized  
✅ Open Graph tags for social sharing  
✅ Canonical URL set  
✅ Structured data ready for Schema.org  
✅ Mobile responsive  
✅ Fast load times  

**To maximize SEO:**
1. Submit sitemap.xml to Google Search Console
2. Get backlinks from relevant cannabis industry sites
3. Update page meta description after launch

---

## 🚦 Testing Before Launch

### 1. Form Test
1. Open page in browser
2. Scroll to "Pilot Program" section
3. Fill out form
4. Submit
5. Check email for form response (Formspree sends confirmation)

### 2. Analytics Test
1. Open page
2. Open DevTools → Network tab
3. Refresh page
4. Check that Google Analytics script loads
5. Visit Google Analytics dashboard (may take 24-48h for data)

### 3. Mobile Test
1. Open page on iPhone/Android
2. Verify layout is responsive
3. Test form on mobile
4. Check navigation

### 4. Lighthouse Audit
1. Open DevTools → Lighthouse
2. Run "Mobile" audit
3. Target scores: Performance >90, SEO >90
4. Fix any issues

---

## 📈 Post-Launch

### Week 1
- Monitor form submissions
- Check Google Analytics for traffic patterns
- Test all CTAs are working

### Week 2+
- Analyze which sections get most engagement
- Update if needed based on data
- Promote on social/email

---

## 🆘 Troubleshooting

**Form not working?**
- Check Formspree endpoint is correct
- Check browser console for errors
- Verify form has required fields filled

**Analytics not showing data?**
- GA ID might be wrong
- Can take 24-48 hours for first data
- Check Google Analytics admin settings

**Styles looking broken?**
- Hard refresh browser (Cmd+Shift+R on Mac, Ctrl+F5 on Windows)
- Clear browser cache
- Check cache headers in your hosting

**Animations not smooth?**
- Check browser is updated
- Disable browser extensions
- Test in Chrome/Safari (best compatibility)

---

## 📞 Support

For deployment help:
- **Vercel:** [vercel.com/docs](https://vercel.com/docs)
- **Netlify:** [netlify.com/docs](https://netlify.com/docs)
- **Formspree:** [formspree.io/documentation](https://formspree.io/documentation)

---

**You're ready to launch!** 🎉
