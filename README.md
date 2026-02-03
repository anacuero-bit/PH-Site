# Pombo & Horowitz - Website + Content System

Immigration law firm website with dynamic content loading, optimized for the 2026 Spanish extraordinary regularization process.

## 🏗️ Architecture

```
ph-site/
├── index.html          # Main landing page with dynamic content
├── blog.html           # Full blog listing with filters
├── content.json        # Dynamic content data (updated by bot)
├── sitemap.xml         # SEO sitemap
├── robots.txt          # SEO robots
├── CNAME               # Custom domain config
└── README.md           # This file
```

## 🚀 Quick Deploy to GitHub Pages

### 1. Create Repository
```bash
# Initialize git
cd ph-site
git init
git add .
git commit -m "Initial site setup"

# Create repo on GitHub, then:
git remote add origin https://github.com/YOUR_USERNAME/ph-site.git
git branch -M main
git push -u origin main
```

### 2. Enable GitHub Pages
1. Go to repo Settings → Pages
2. Source: Deploy from branch
3. Branch: main, folder: / (root)
4. Save

### 3. Configure Custom Domain
1. In GitHub Pages settings, add custom domain: `pombohorowitz.es`
2. At your DNS provider, add:
   - A record: `@` → `185.199.108.153`
   - A record: `@` → `185.199.109.153`
   - A record: `@` → `185.199.110.153`
   - A record: `@` → `185.199.111.153`
   - CNAME record: `www` → `YOUR_USERNAME.github.io`

## 📝 Content Structure (content.json)

The site dynamically loads content from `content.json`. The content bot will update this file.

### Articles
```json
{
  "articles": [
    {
      "id": "unique-slug",
      "slug": "unique-slug",
      "title": "Article Title",
      "excerpt": "Short description...",
      "content": "<p>Full HTML content...</p>",
      "category": "regularizacion|documentacion|consejos|noticias",
      "date": "2026-02-03",
      "author": "Author Name",
      "readTime": "5 min",
      "featured": true|false
    }
  ]
}
```

### FAQs
```json
{
  "faqs": [
    {
      "id": "faq-1",
      "question": "Question text?",
      "answer": "Answer text.",
      "category": "plazos|requisitos|documentacion|proceso"
    }
  ]
}
```

### Updates (News Banner)
```json
{
  "updates": [
    {
      "id": "update-1",
      "date": "2026-02-03",
      "type": "info|urgente",
      "title": "Update Title",
      "message": "Update message text."
    }
  ]
}
```

### Stats (Auto-updated)
```json
{
  "stats": {
    "cases_resolved": 12847,
    "years_experience": 38,
    "success_rate": 97,
    "clients_regularization": 312
  }
}
```

## 🤖 Content Bot Integration

The content bot will update `content.json` via GitHub API:

```python
import requests
import base64
import json

GITHUB_TOKEN = "your_token"
REPO = "your_username/ph-site"

def update_content(new_content):
    # Get current file SHA
    url = f"https://api.github.com/repos/{REPO}/contents/content.json"
    headers = {"Authorization": f"token {GITHUB_TOKEN}"}
    
    response = requests.get(url, headers=headers)
    current_sha = response.json()["sha"]
    
    # Update file
    content_b64 = base64.b64encode(json.dumps(new_content, indent=2).encode()).decode()
    
    data = {
        "message": "Update content",
        "content": content_b64,
        "sha": current_sha
    }
    
    response = requests.put(url, headers=headers, json=data)
    return response.status_code == 200
```

## 🎯 Key Features

### Dynamic Content Loading
- Articles loaded from `content.json`
- FAQs loaded from `content.json`
- News updates scroll banner
- No page reload needed

### SEO Optimized
- Spanish language meta tags
- Open Graph tags
- Semantic HTML structure
- Sitemap and robots.txt
- Fast loading (no framework overhead)

### Mobile-First Design
- Responsive layout
- Touch-friendly navigation
- WhatsApp integration
- Click-to-call buttons

### Conversion Focused
- Eligibility checker widget
- Countdown timer (June 30, 2026)
- WhatsApp CTA buttons
- Clear call-to-actions

## 📱 Contact Integration

Update these placeholders in index.html:
- Phone: `+34915551234` → Your actual number
- WhatsApp: `34600000000` → Your WhatsApp number
- Email: `info@pombohorowitz.es` → Your email
- Address: Update in footer

## 🔄 Content Update Workflow

1. **Manual**: Edit `content.json` directly, commit to GitHub
2. **Bot (Recommended)**: Content bot fetches news, generates articles, pushes to GitHub
3. **Scheduled**: Bot runs daily/weekly cron jobs

## 📊 Analytics Setup

Add to `<head>` in both HTML files:

```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

## 🛠️ Development

To test locally:
```bash
# Python
python -m http.server 8000

# Node
npx serve .

# Then open http://localhost:8000
```

## 📋 Next Steps

1. **Deploy site** → GitHub Pages
2. **Configure domain** → DNS settings
3. **Update contacts** → Phone, WhatsApp, email
4. **Add analytics** → Google Analytics
5. **Deploy bot** → Client-facing Telegram bot
6. **Deploy content bot** → Automated content generation

---

Built for Pombo & Horowitz Abogados | Regularización 2026
