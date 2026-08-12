# OB Promotions — Assets

This directory contains the publicly served static assets for the **OB Promotions** website.

OB Promotions is a boxing promotions website focused on helping boxers apply for fights, discover upcoming cards, and learn about the services offered by the promotion.

The website includes promotional imagery, branding assets, icons, social graphics, and a video background for the homepage hero section.

> **Important:** This directory is part of the public asset CDN repository. Do not store private, sensitive, or confidential files here.

---

## Hero Video

The homepage hero uses a full-bleed video background behind the primary headline and CTA.

The video is intended to function as **visual texture**, not as a source of information. All important messaging is rendered as HTML text over the video.

### Recommended location

```text
video/hero/
├── hero.webm
├── hero.mp4
└── hero-poster.webp
```

### Required formats

| Asset              | Format      | Purpose                                 |
| ------------------ | ----------- | --------------------------------------- |
| `hero.webm`        | WebM / VP9  | Preferred modern browser format         |
| `hero.mp4`         | MP4 / H.264 | Fallback format                         |
| `hero-poster.webp` | WebP        | Initial/poster image before video loads |

The website should provide WebM first, followed by MP4.

```html
<video autoplay muted loop playsinline preload="none">
  <source src="hero.webm" type="video/webm" />
  <source src="hero.mp4" type="video/mp4" />
</video>
```

---

## Hero Video Specifications

The current project specification requires:

* Duration: **8–14 seconds**
* Seamless loop
* Master resolution: **1920×1080**
* Mobile variant: **1280×720**
* Desktop target size: **≤ 2.5 MB**
* Mobile target size: **≤ 1.2 MB**
* Video format: **H.264 MP4 + VP9 WebM**
* No audio track
* `autoplay`
* `muted`
* `loop`
* `playsinline`
* `preload="none"`

The audio track should be removed during encoding rather than relying only on the `muted` attribute.

---

## Hero Video Content

The footage should be:

* Slow-paced
* Tight/framed closely
* High contrast
* Visually compatible with text overlay

Suitable footage includes:

* Boxing wraps being put on
* Rope skipping
* Fighter shoulders in low light
* Heavy-bag work
* Training footage shot from behind
* Close-up gym footage

Avoid footage containing:

* Fast cuts
* Crowd scenes
* Scoreboards
* Important subjects directly behind the headline
* Visual elements that compete heavily with the overlay text

The center portion of the video should remain relatively clear because the hero headline is positioned over the footage.

---

# Hero Poster

The first frame of the hero video should be exported as:

```text
video/hero/hero-poster.webp
```

The poster is used to allow the hero to render visually before the video is loaded.

The poster should also be used when:

* The visitor prefers reduced motion
* The visitor is on a small/mobile viewport
* `navigator.connection.saveData` is enabled

The project specification specifically requires the video not to load under `prefers-reduced-motion: reduce`, and recommends serving only the poster below 768px or when Save-Data is enabled.

---

# Images

General OB Promotions imagery belongs inside:

```text
images/
```

Use subdirectories when there are multiple types of images.

### Hero imagery

```text
images/hero/
```

### Event imagery

```text
images/events/
```

### Fighter imagery

```text
images/fighters/
```

### Promotional graphics

```text
images/promotions/
```

### Background imagery

```text
images/backgrounds/
```

---

# Logos

Brand identity assets belong inside:

```text
logos/
```

Recommended naming:

```text
logos/
├── logo.svg
├── logo-dark.svg
├── logo-light.svg
└── logo-mark.svg
```

Use SVG whenever the original logo is vector-based.

Do not create multiple versions of the same logo unless they serve a specific use case.

---

# Icons

UI and application icons belong inside:

```text
icons/
```

Examples:

```text
icons/
├── favicon.png
├── app-icon.png
└── social-icon.svg
```

---

# Social / Open Graph Assets

Assets used for social sharing and Open Graph metadata belong inside:

```text
social/
```

The homepage currently specifies an OG image at:

```text
1200 × 630
```

The intended design uses a video poster frame with the OB Promotions wordmark positioned at the bottom-left.

Recommended filename:

```text
social/og-image.png
```

---

# Naming Convention

Use lowercase **kebab-case** for filenames and directories.

### Recommended

```text
hero.webm
hero.mp4
hero-poster.webp
logo-dark.svg
fight-night-01.jpg
fighter-profile-01.jpg
og-image.png
```

### Avoid

```text
Hero Video FINAL.mp4
IMG_4829.JPG
New Logo Final FINAL.svg
boxing video 2.mp4
```

Consistent naming makes CDN URLs easier to read and maintain.

---

# CDN Usage

Assets in this directory are served through the repository's Statically CDN.

The general URL structure is:

```text
https://cdn.statically.io/gh/USERNAME/REPOSITORY@main/ob-promotions/PATH
```

For example:

```text
ob-promotions/video/hero/hero-poster.webp
```

becomes:

```text
https://cdn.statically.io/gh/USERNAME/REPOSITORY@main/ob-promotions/video/hero/hero-poster.webp
```

Likewise:

```text
ob-promotions/logos/logo.svg
```

becomes:

```text
https://cdn.statically.io/gh/USERNAME/REPOSITORY@main/ob-promotions/logos/logo.svg
```

These URLs can then be used directly by the OB Promotions website.

---

# Asset Lifecycle

When adding an asset:

```text
Create
  ↓
Optimize
  ↓
Place in appropriate directory
  ↓
Commit to Git
  ↓
Push to GitHub
  ↓
Serve through Statically
  ↓
Use CDN URL in OB Promotions
```

---

# Production Considerations

### Optimize before uploading

Images and videos should be optimized before being committed.

For example:

```text
Original image
    ↓
Resize if necessary
    ↓
Compress
    ↓
Convert to appropriate web format
    ↓
Upload
```

Avoid using this repository for storing massive original design files.

---

### Do not store secrets

Never put the following in this directory:

```text
.env
.env.local
API keys
API secrets
passwords
private credentials
private client documents
access tokens
```

Everything here should be treated as publicly accessible.

---

### Do not store source project files

This repository is an **asset repository**, not the main OB Promotions application repository.

Do not add:

```text
src/
node_modules/
.next/
dist/
package.json
.env
```

unless a file is specifically intended to be publicly served as an asset.

---

# Current Website Asset Requirements

The current OB Promotions website specification identifies several asset-dependent areas:

### Homepage Hero

```text
video/hero/
```

Full-bleed boxing video background with a poster fallback.

### Branding

```text
logos/
```

Used throughout the website.

### Events

```text
images/events/
```

For upcoming fight cards and promotional material.

### Fighters

```text
images/fighters/
```

For boxer-related content when verified fighter information and imagery are available.

### Promotional Material

```text
images/promotions/
```

For marketing campaigns, event graphics, posters, and related promotional content.

### Social Sharing

```text
social/
```

For OG/social preview imagery.

---

# Important Content Rule

The website specification explicitly requires claims about records, results, rosters, events, venues, and similar information to be verifiable.

Therefore, **do not add unverified fighter names, records, event information, venue information, titles, or promotional claims simply to fill this directory.**

The project document currently contains placeholders for information that still needs to be confirmed by the client.

---

# Project Reference

**Project:** OB Promotions
**Type:** Boxing Promotions / Marketing Website
**Primary purpose:** Promote boxing services, upcoming events, and provide an application path for boxers who want to fight on OB Promotions cards.

### Primary website actions

```text
Apply to fight
See our packages
View upcoming card
Learn about OB Promotions
```

The homepage's primary positioning is:

> Fights that build careers

The website describes OB Promotions as a boxing promotion focused on matchmaking, event promotion, career management, and related fighter support, although the final package names still need client confirmation.

---

# Status

**Asset repository status:** Active / In Development

### Known required assets

* [ ] OB Promotions logo
* [ ] Hero video — WebM
* [ ] Hero video — MP4
* [ ] Hero poster — WebP
* [ ] Favicon
* [ ] OG image
* [ ] Event imagery
* [ ] Fighter imagery
* [ ] Promotional graphics

### Pending client information

The project specification identifies the following information as still outstanding:

* Actual service/package names
* Next event details, if applicable
* Verified proof/statistics
* Application response time
* Hero video source/footage

These should be confirmed before the corresponding production assets are finalized.
