# DataLabSync - Netlify Deployment Package

## 📦 Contents

| File | Description |
|------|-------------|
| `index.html` | Main landing page with Unsplash photography |
| `onboarding.html` | Post-signup quiz and onboarding flow |
| `netlify.toml` | Netlify build configuration |
| `_headers` | CDN caching and security headers |
| `_redirects` | URL redirects (www → non-www) |
| `robots.txt` | Search engine crawling rules |
| `sitemap.xml` | SEO sitemap |
| `EMAIL_SEQUENCES.md` | Email marketing templates by segment |
| `ANALYTICS_SCHEMA.md` | Data model and analytics documentation |

---

## 🚀 Deployment

### Option 1: Drag & Drop
1. Go to [app.netlify.com](https://app.netlify.com)
2. Drag this entire folder onto the dashboard
3. Done! Your site is live.

### Option 2: Netlify CLI
```bash
npm install -g netlify-cli
netlify login
netlify deploy --prod
```

### Option 3: Git Integration
1. Push this folder to a GitHub/GitLab repo
2. Connect the repo to Netlify
3. Automatic deploys on every push

---

## 🔧 Configuration

### Formspree
Both forms submit to Formspree. Update the endpoint in both files:
- `index.html` (line ~2095): `https://formspree.io/f/xbjnzxyz`
- `onboarding.html` (line ~850): `https://formspree.io/f/xbjnzxyz`

Replace `xbjnzxyz` with your actual Formspree form ID.

### Custom Domain
1. In Netlify dashboard, go to Domain Settings
2. Add your custom domain (e.g., `datalabsync.com`)
3. Update `sitemap.xml` and `_redirects` with your domain

### Analytics (Optional)
Add your analytics script before `</head>` in both HTML files:
```html
<!-- Plausible -->
<script defer data-domain="datalabsync.com" src="https://plausible.io/js/script.js"></script>

<!-- Or Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXX"></script>
```

---

## 📊 User Flow

```
Landing Page (index.html)
    ↓
User submits email
    ↓
Redirect to Onboarding (onboarding.html)
    ↓
Quiz: 7 questions
    ↓
Thank You + Email Confirmation
```

### Data Captured

| Question | Field Name | Purpose |
|----------|------------|---------|
| Role | `role` | Segmentation |
| Current Tools | `currentTools` | Integration priority |
| Frustration | `biggestFrustration` | Roadmap |
| Time Spent | `timeSpentOnAdmin` | ROI proof |
| Engagement | `engagementPreference` | Sales pipeline |
| Pricing | `pricingWillingness` | Pricing strategy |
| Feedback | `openFeedback` | Qualitative insights |

---

## 📧 Email Integration

See `EMAIL_SEQUENCES.md` for complete email templates.

### Recommended Setup
1. Create Formspree form
2. Connect Formspree to Zapier
3. Route to ConvertKit/Mailchimp based on `engagementPreference` field
4. Trigger appropriate email sequence

### Segmentation Rules
- **Demo Seekers**: `engagementPreference` = "I'd love to see an early demo"
- **Pilot Candidates**: `engagementPreference` contains "pilot" or "team"
- **High Value**: `pricingWillingness` >= "$300" AND `timeSpentOnAdmin` >= "10 hours"

---

## 🎨 Brand System

### Typography
- **Headings**: Space Grotesk (600 weight)
- **Body**: Inter (400/500 weight)

### Colors
- Primary: `#0550ae`
- Success: `#1a7f37`
- Text: `#1f2328`
- Muted: `#8b949e`
- Background: `#fafbfc`

### Spacing Scale
4px → 8px → 12px → 16px → 24px → 32px → 48px → 64px

---

## 🔒 Security Headers

Configured in `_headers` and `netlify.toml`:
- X-Frame-Options: DENY
- X-Content-Type-Options: nosniff
- Referrer-Policy: strict-origin-when-cross-origin

---

## 📱 Responsive Breakpoints

- Desktop: > 1024px
- Tablet: 768px - 1024px
- Mobile: < 768px

---

## ✅ Checklist Before Launch

- [ ] Update Formspree form ID
- [ ] Test form submission
- [ ] Add custom domain
- [ ] Configure email automation
- [ ] Add analytics
- [ ] Test on mobile devices
- [ ] Review all copy for accuracy
- [ ] Update sitemap with final domain

---

## 🆘 Support

Built with care for DataLabSync.
Questions? Review the inline code comments or reach out.
