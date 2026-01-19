# 🚀 Setup Guide: ishanyatea-ship-it Repository

**Target Repository:** https://github.com/ishanyatea-ship-it  
**Domain:** ishanyatea.com  
**Updated:** January 19, 2026

## 🎯 Repository Setup Steps

### Step 1: Create GitHub Repository
1. **Sign in to GitHub** using the `ishanyatea-ship-it` account
2. **Create New Repository:**
   - Repository name: `ishanyatea-ship-it`  
   - Description: `🍃 Ishanya Tea - Premium Tea Business Website`
   - Set as: **Public** (required for GitHub Pages)
   - Initialize with README: **Yes**
   - Add .gitignore: **None** (we'll provide custom)
   - License: **MIT** (recommended)

### Step 2: Clone and Setup Local Repository
```powershell
# Navigate to your website projects directory
cd "c:\ObsidianMCP\Personal\07-JPNV\Website-Projects\GitHub-Repos"

# Clone the new repository
git clone https://github.com/ishanyatea-ship-it.git
cd ishanyatea-ship-it

# Create the required folder structure
mkdir -p data, images, config, .github/workflows
```

### Step 3: Add Website Infrastructure Files

#### Create GitHub Actions Workflow
Create: `.github/workflows/build-deploy.yml`
```yaml
name: Build and Deploy Website

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build-deploy:
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    
    steps:
    - name: Checkout repository
      uses: actions/checkout@v4
      
    - name: Setup Node.js
      uses: actions/setup-node@v4
      with:
        node-version: '18'
        
    - name: Clone MCP Website Builder
      run: |
        git clone https://github.com/pmkhairnarr/spreadsheet-website-builder-mcp.git builder
        cd builder
        npm install
        
    - name: Process Data and Build Website
      run: |
        cd builder
        node src/index.js --input ../data --output ../dist --config ../config/website-config.json
        
    - name: Setup Pages
      uses: actions/configure-pages@v4
      
    - name: Upload artifact
      uses: actions/upload-pages-artifact@v3
      with:
        path: './dist'
        
    - name: Deploy to GitHub Pages
      id: deployment
      uses: actions/deploy-pages@v4
```

#### Create Configuration Files
Create: `config/website-config.json`
```json
{
  "site": {
    "title": "Ishanya Tea - Premium Tea Experience",
    "description": "Discover premium tea varieties and personalized tea experiences",
    "baseUrl": "https://ishanyatea.com",
    "theme": "modern-tea"
  },
  "colors": {
    "primary": "#2D5016",
    "secondary": "#8FBC8F", 
    "accent": "#DAA520",
    "background": "#F8F9FA"
  },
  "features": {
    "productCatalog": true,
    "contactForm": true,
    "imageGallery": true,
    "testimonials": true,
    "seo": true
  },
  "contact": {
    "email": "info@ishanyatea.com",
    "phone": "(555) 123-4567",
    "address": "123 Tea Street, City, State 12345"
  }
}
```

#### Add Domain Configuration
Create: `CNAME`
```
ishanyatea.com
```

#### Create Sample Data Structure
Create: `data/README.md`
```markdown
# Data Files Directory

Upload your Excel files (.xlsx) or CSV files here:

## Required Files:
- `products.xlsx` or `products.csv` - Tea products data
- `services.xlsx` or `services.csv` - Services offered  
- `about.xlsx` or `about.csv` - Company information
- `contact.xlsx` or `contact.csv` - Contact details
- `gallery.xlsx` or `gallery.csv` - Image gallery data

## Alternative:
- `tea-business.xlsx` - Single file with multiple sheets

The GitHub Action will automatically process any data files uploaded here.
```

### Step 4: Enable GitHub Pages
1. Go to: `https://github.com/ishanyatea-ship-it/settings/pages`
2. **Source:** Deploy from a branch → `gh-pages` 
3. **Custom domain:** Enter `ishanyatea.com`
4. **Enforce HTTPS:** ✅ Check this option
5. **Save** settings

## 📋 Quick Setup Commands

Run these commands after creating the repository:

```powershell
# Navigate and setup
cd "c:\ObsidianMCP\Personal\07-JPNV\Website-Projects\GitHub-Repos"
git clone https://github.com/ishanyatea-ship-it.git
cd ishanyatea-ship-it

# Create directory structure
New-Item -ItemType Directory -Path "data", "images", "config", ".github", ".github/workflows" -Force

# Copy your existing content
Copy-Item "../../Ishayna Tea/tea-products-sample.csv" "./data/products.csv"
Copy-Item "../../Ishayna Tea/images/*" "./images/" -Recurse -Force

# Create and add the workflow file (copy the YAML above)
# Create and add the config file (copy the JSON above)

# Add domain configuration
"ishanyatea.com" | Out-File -FilePath "CNAME" -Encoding utf8

# Initial commit
git add .
git commit -m "Initial setup: website infrastructure and sample data"
git push origin main
```

## 🔧 GoDaddy DNS Configuration

Update these DNS records in your GoDaddy account:

| Type | Name | Value | TTL |
|------|------|-------|-----|
| **CNAME** | www | `ishanyatea-ship-it.github.io` | 1 hour |
| **A** | @ | `185.199.108.153` | 1 hour |
| **A** | @ | `185.199.109.153` | 1 hour |
| **A** | @ | `185.199.110.153` | 1 hour |
| **A** | @ | `185.199.111.153` | 1 hour |

## 🎯 Expected Results

After setup completion:
- ✅ **Repository:** https://github.com/ishanyatea-ship-it
- ✅ **GitHub Pages:** https://ishanyatea-ship-it.github.io  
- ✅ **Custom Domain:** https://ishanyatea.com (after DNS propagation)
- ✅ **Automatic Builds:** Triggered on every content update
- ✅ **SSL Certificate:** Automatically provided by GitHub

## 🚀 Content Upload Process

1. **Add your Excel file** to `/data/` directory
2. **Upload images** to `/images/` directory  
3. **Commit and push** changes
4. **GitHub Actions** automatically builds and deploys
5. **Website updates** live in 2-5 minutes

---

**Ready to proceed?** Follow the steps above, and you'll have your professional tea business website live at `ishanyatea.com`! 🍃