# Personal Asset CDN

A personal repository for storing and serving static assets through [Statically](https://statically.io/) as a CDN.

This repository is **not an application or source-code repository**. It is a centralized asset library for files that need to be publicly accessible from websites, applications, documentation, social previews, emails, and other projects.

Typical assets include:

* Images
* Logos
* Icons
* SVGs
* Favicons
* Screenshots
* Marketing graphics
* Project assets
* Public JSON/data files
* Other static files

---

## How It Works

The flow is simple:

```text
Local File
    ↓
GitHub Repository
    ↓
Statically CDN
    ↓
Your Application / Website
```

Files are organized inside this repository by project.

For example:

```text
asset-cdn/
├── ob-promotions/
│   ├── logo/
│   │   ├── logo.svg
│   │   └── logo-dark.svg
│   ├── images/
│   │   ├── hero.png
│   │   ├── flyer-01.jpg
│   │   └── flyer-02.jpg
│   └── icons/
│       └── favicon.png
│
└── portfolio/
    ├── screenshots/
    └── projects/
```

Once a file is pushed to GitHub, it can be served through Statically using the file's repository path.

---

# Repository Structure

Projects should be stored in their own top-level directory.

### Recommended structure

```text
/
├── project-name/
│   ├── images/
│   ├── logos/
│   ├── icons/
│   ├── screenshots/
│   └── ...
│
├── another-project/
│   ├── images/
│   └── ...
│
└── personal/
    ├── images/
    └── ...
```

### Example

For the **OB Promotions** project:

```text
ob-promotions/
├── logo/
│   ├── logo.svg
│   ├── logo-dark.svg
│   └── logo-mark.svg
│
├── images/
│   ├── hero.png
│   ├── promotion-01.jpg
│   ├── promotion-02.jpg
│   └── background.jpg
│
├── icons/
│   ├── favicon.png
│   └── app-icon.png
│
└── screenshots/
    ├── desktop.png
    └── mobile.png
```

This keeps assets isolated and makes them easy to find later.

---

# Naming Convention

Use lowercase **kebab-case** for directories and files.

### Good

```text
ob-promotions/
hero-image.png
logo-dark.svg
promotion-01.jpg
mobile-banner.png
```

### Avoid

```text
OB Promotions/
Hero Image.png
Logo Dark.svg
promotion final FINAL 2.png
```

The goal is to keep CDN URLs predictable and easy to read.

---

# Adding a New Project

When starting a new project:

1. Create a top-level directory.
2. Use the project's slug as the directory name.
3. Create categories where necessary.
4. Add the assets.
5. Commit and push the changes.

Example:

```bash
mkdir -p ob-promotions/{logo,images,icons,screenshots}
```

Then add the files:

```text
ob-promotions/
├── logo/
├── images/
├── icons/
└── screenshots/
```

---

# Serving Files Through Statically

Statically provides a CDN URL for files stored in public GitHub repositories.

The general format is:

```text
https://cdn.statically.io/gh/USERNAME/REPOSITORY@BRANCH/PATH_TO_FILE
```

For example:

```text
https://cdn.statically.io/gh/adedotun/asset-cdn@main/ob-promotions/images/hero.png
```

The important part is that the path after the branch matches the exact path inside this repository.

### Repository

```text
ob-promotions/images/hero.png
```

### CDN

```text
https://cdn.statically.io/gh/adedotun/asset-cdn@main/ob-promotions/images/hero.png
```

---

# Using Assets in Projects

Once a CDN URL has been generated, use it anywhere a normal public URL is accepted.

### HTML

```html
<img
  src="https://cdn.statically.io/gh/adedotun/asset-cdn@main/ob-promotions/images/hero.png"
  alt="OB Promotions"
/>
```

### CSS

```css
.hero {
  background-image: url("https://cdn.statically.io/gh/adedotun/asset-cdn@main/ob-promotions/images/hero.png");
}
```

### React

```tsx
<img
  src="https://cdn.statically.io/gh/adedotun/asset-cdn@main/ob-promotions/images/hero.png"
  alt="OB Promotions"
/>
```

### Next.js

```tsx
<Image
  src="https://cdn.statically.io/gh/adedotun/asset-cdn@main/ob-promotions/images/hero.png"
  alt="OB Promotions"
  width={1200}
  height={800}
/>
```

If using Next.js, remember to configure the CDN hostname in `next.config.ts`.

---

# Git Workflow

Assets should be added through Git like any other repository content.

### Add an asset

```bash
git add ob-promotions/images/hero.png
```

### Commit

```bash
git commit -m "assets: add OB Promotions hero image"
```

### Push

```bash
git push origin main
```

After the file is available in the public GitHub repository, it can be requested through Statically.

---

# Versioning

For assets that need stable URLs, prefer using a **Git tag or commit** instead of relying on `main`.

For example:

```text
https://cdn.statically.io/gh/adedotun/asset-cdn@v1.0.0/ob-promotions/images/hero.png
```

This provides a stable reference to a specific version of the repository.

Use `main` when you intentionally want the CDN URL to follow the latest version of the file.

### Recommended approach

For development:

```text
@main
```

For production assets that should not unexpectedly change:

```text
@v1.0.0
```

or another immutable Git reference.

---

# Asset Categories

Use categories only when they provide meaningful organization.

Recommended categories:

| Directory      | Purpose                                 |
| -------------- | --------------------------------------- |
| `images/`      | General images and graphics             |
| `logo/`        | Brand logos and marks                   |
| `icons/`       | Icons and UI graphics                   |
| `screenshots/` | Product/application screenshots         |
| `banners/`     | Promotional and banner graphics         |
| `avatars/`     | Profile/avatar images                   |
| `documents/`   | Public documents and downloadable files |
| `fonts/`       | Public font files, when appropriate     |
| `data/`        | Public JSON, CSV, or other data files   |

Do not create unnecessary nested directories.

Prefer:

```text
ob-promotions/images/hero.png
```

over:

```text
ob-promotions/assets/marketing/images/website/homepage/hero/hero-final.png
```

Keep the structure useful rather than excessively deep.

---

# Rules

## 1. Only public assets

This repository is public because Statically requires public repositories.

**Never store:**

* API keys
* Passwords
* Access tokens
* Private documents
* Credentials
* Environment files
* Private customer information
* Sensitive project information

If a file should not be publicly accessible, it does not belong here.

---

## 2. Keep files reasonably sized

Statically currently documents a **25 MB maximum file size per file**.

However, large files should generally be optimized before being added.

For images:

* Compress PNG/JPEG files where possible.
* Prefer WebP or AVIF for web images when appropriate.
* Avoid uploading unnecessarily large source images.
* Keep original design/source files in the actual project repository instead.

---

## 3. This is an asset repository, not a backup repository

Do not use this repository as general cloud storage.

Store assets that are intentionally meant to be publicly served.

---

## 4. Do not overwrite production assets unnecessarily

If an asset is already being used in production, avoid replacing it unexpectedly.

Instead of:

```text
hero.png
```

consider versioning the asset:

```text
hero-v2.png
```

or use a versioned Git reference.

This reduces the possibility of an existing application unexpectedly receiving a different asset.

---

# Quick Reference

### Add an asset

```text
1. Create project directory
2. Create appropriate category
3. Add asset
4. Commit
5. Push
```

### Example

```text
ob-promotions/
└── images/
    └── hero.png
```

### CDN URL

```text
https://cdn.statically.io/gh/USERNAME/REPOSITORY@main/ob-promotions/images/hero.png
```

### Production URL

```text
https://cdn.statically.io/gh/USERNAME/REPOSITORY@v1.0.0/ob-promotions/images/hero.png
```

---

# Project Index

Keep a simple list of the projects currently using this repository.

| Project       | Directory        | Description                           |
| ------------- | ---------------- | ------------------------------------- |
| OB Promotions | `ob-promotions/` | OB Promotions project assets          |
| Portfolio     | `portfolio/`     | Portfolio and personal website assets |

Add new projects to this table when their asset directory is created.

---

# Philosophy

This repository follows one simple principle:

> **Store once. Serve anywhere.**

GitHub is the source of truth.

Statically is the delivery layer.

Projects consume the resulting public CDN URLs.

The repository should therefore remain organized, predictable, lightweight, and strictly focused on publicly accessible static assets.
