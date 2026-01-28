# GitHub Actions Deployment Workflow

Belajar CI/CD dengan GitHub Actions untuk auto-deploy website ke GitHub Pages.

Project reference: [roadmap.sh/projects/github-actions-deployment-workflow](https://roadmap.sh/projects/github-actions-deployment-workflow)

---

## 🌐 Live Demo

**https://amirkurniawan.github.io/gh-deployment-workflow/**

---

## ✨ Features

- ✅ Auto-deploy on push to `main` branch
- ✅ Only triggers when `index.html` is changed
- ✅ Manual deployment via workflow_dispatch
- ✅ Concurrent deployment protection
- ✅ DevOps portfolio landing page

---

## 📁 Project Structure

```
gh-deployment-workflow/
├── .github/
│   └── workflows/
│       └── deploy.yml    # GitHub Actions workflow
├── index.html            # Website content
└── README.md             # Documentation
```

---

## 🚀 How It Works

```
┌─────────────────────┐
│  Push to main       │
│  (index.html)       │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  GitHub Actions     │
│  Triggered          │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Build Job          │
│  - Checkout code    │
│  - Upload artifact  │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Deploy Job         │
│  - Deploy to Pages  │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  🎉 Live Website!   │
│  github.io/...      │
└─────────────────────┘
```

---

## 📝 Workflow Explained

### deploy.yml

```yaml
name: Deploy to GitHub Pages

# Trigger conditions
on:
  push:
    branches:
      - main
    paths:
      - 'index.html'  # Only when this file changes
  workflow_dispatch:   # Manual trigger

# Required permissions
permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    # Build and upload artifact
    
  deploy:
    # Deploy to GitHub Pages
```

### Key Concepts

| Concept | Description |
|---------|-------------|
| `on.push.paths` | Only trigger when specific files change |
| `workflow_dispatch` | Enable manual trigger from UI |
| `permissions` | Required for GitHub Pages deployment |
| `concurrency` | Prevent multiple deployments running |
| `needs: build` | Deploy job waits for build job |

---

## 🛠️ Setup Instructions

### 1. Create Repository

```bash
# Create new repo on GitHub named: gh-deployment-workflow
# Clone it
git clone https://github.com/YOUR_USERNAME/gh-deployment-workflow.git
cd gh-deployment-workflow
```

### 2. Add Files

Copy semua file dari project ini:
- `index.html`
- `.github/workflows/deploy.yml`
- `README.md`

### 3. Enable GitHub Pages

1. Go to repository **Settings**
2. Click **Pages** (sidebar)
3. Source: **GitHub Actions**

![GitHub Pages Settings](https://docs.github.com/assets/cb-27697/mw-1440/images/help/pages/pages-source-actions.webp)

### 4. Push and Deploy

```bash
git add .
git commit -m "Initial commit: Setup GitHub Pages deployment"
git push origin main
```

### 5. Check Deployment

- Go to **Actions** tab → See workflow running
- After complete, visit: `https://YOUR_USERNAME.github.io/gh-deployment-workflow/`

---

## 🔄 Trigger Workflow

### Automatic Trigger

Edit `index.html` dan push:

```bash
# Edit index.html
nano index.html

# Commit and push
git add index.html
git commit -m "Update website content"
git push origin main
```

Workflow akan otomatis berjalan.

### Manual Trigger

1. Go to **Actions** tab
2. Select **Deploy to GitHub Pages** workflow
3. Click **Run workflow**
4. Select branch `main`
5. Click **Run workflow**

---

## 📊 Check Workflow Status

### Via GitHub UI

1. Go to repository
2. Click **Actions** tab
3. See all workflow runs

### Via Badge (Optional)

Add to README:

```markdown
![Deploy Status](https://github.com/YOUR_USERNAME/gh-deployment-workflow/actions/workflows/deploy.yml/badge.svg)
```

---

## 🐛 Troubleshooting

### Workflow Not Triggering

- Pastikan file `.github/workflows/deploy.yml` ada
- Pastikan push ke branch `main`
- Pastikan `index.html` yang berubah

### 404 on GitHub Pages

- Check Settings → Pages → Source = GitHub Actions
- Tunggu beberapa menit setelah deploy
- Clear browser cache

### Permission Denied

Pastikan permissions di workflow:

```yaml
permissions:
  contents: read
  pages: write
  id-token: write
```

---

## 📚 Concepts Learned

1. **GitHub Actions** - Workflow automation
2. **CI/CD** - Continuous Integration/Deployment
3. **GitHub Pages** - Static site hosting
4. **YAML Syntax** - Workflow configuration
5. **Triggers** - Event-based automation
6. **Artifacts** - Build outputs

---

## 🔗 Related Links

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [Workflow Syntax Reference](https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions)
- [DevOps Labs Repository](https://github.com/amirkurniawan/devops-labs)

---

## 🎯 Stretch Goals

- [ ] Use static site generator (Hugo/Jekyll)
- [ ] Add custom domain
- [ ] Add build step (minify, optimize)
- [ ] Add testing before deploy
- [ ] Slack/Discord notification on deploy

---

*Project completed as part of DevOps learning journey*

![Deploy Status](https://github.com/amirkurniawan/gh-deployment-workflow/actions/workflows/deploy.yml/badge.svg)
