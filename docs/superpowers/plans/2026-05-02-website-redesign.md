# Website Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Modernise sajnikanth.com with a dark card layout, circular profile photo, system-ui font, and blurred background — all in a single `index.html`, no frameworks.

**Architecture:** Single HTML5 file with inline CSS. Background photo is CSS-blurred and darkened. Content is a centered dark card with a header row (photo + name + role), bio, social icons, presentations, and footer.

**Tech Stack:** Plain HTML5, inline CSS, no JavaScript except the existing GA snippet.

---

## File Structure

| File | Action | Responsibility |
|---|---|---|
| `index.html` | Rewrite | Entire page — markup + styles |
| `images/profile.jpg` | Add | New circular profile photo |
| `images/background_small.jpeg` | Delete | No longer needed |

---

### Task 1: Copy the new profile photo

**Files:**
- Add: `images/profile.jpg`

- [ ] **Step 1: Copy the photo**

The source photo is at:
`/Users/ssuriyanarayanan/Library/CloudStorage/Dropbox/Stuff/Documents/19800913 - Sajnikanth/Photos/Profile - AI Upscaled.jpeg`

```bash
cp "/Users/ssuriyanarayanan/Library/CloudStorage/Dropbox/Stuff/Documents/19800913 - Sajnikanth/Photos/Profile - AI Upscaled.jpeg" \
  /Users/ssuriyanarayanan/Library/CloudStorage/Dropbox/repo/domains/sajnikanth.com/images/profile.jpg
```

- [ ] **Step 2: Verify the file exists**

```bash
ls -lh /Users/ssuriyanarayanan/Library/CloudStorage/Dropbox/repo/domains/sajnikanth.com/images/profile.jpg
```

Expected: file listed, size > 0

- [ ] **Step 3: Commit**

```bash
cd /Users/ssuriyanarayanan/Library/CloudStorage/Dropbox/repo/domains/sajnikanth.com
git add images/profile.jpg
git commit -m "Add new profile photo"
```

---

### Task 2: Delete unused image

**Files:**
- Delete: `images/background_small.jpeg`

- [ ] **Step 1: Remove the file**

```bash
git rm /Users/ssuriyanarayanan/Library/CloudStorage/Dropbox/repo/domains/sajnikanth.com/images/background_small.jpeg
```

- [ ] **Step 2: Commit**

```bash
cd /Users/ssuriyanarayanan/Library/CloudStorage/Dropbox/repo/domains/sajnikanth.com
git commit -m "Remove unused background_small.jpeg"
```

---

### Task 3: Rewrite index.html

**Files:**
- Rewrite: `index.html`

This is the main task. Replace the entire file with the new design.

- [ ] **Step 1: Verify the current file before touching it**

```bash
wc -l /Users/ssuriyanarayanan/Library/CloudStorage/Dropbox/repo/domains/sajnikanth.com/index.html
```

Expected: ~200 lines (confirms you're editing the right file)

- [ ] **Step 2: Write the new index.html**

Write the following content to `index.html` (full file — not a patch):

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Sajnikanth Suriyanarayanan</title>
  <link rel="icon" type="image/png" href="images/favicon.png" />
  <style>
    *, *::before, *::after {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    html, body {
      height: 100%;
    }

    body {
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      font-size: 14px;
      font-weight: 400;
      color: #cccccc;
      background-color: #000;
      display: flex;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
      padding: 24px;
    }

    .bg {
      position: fixed;
      inset: 0;
      background: url(images/background.jpeg) center / cover no-repeat;
      filter: blur(20px) brightness(0.15);
      transform: scale(1.05);
      z-index: 0;
    }

    .card {
      position: relative;
      z-index: 1;
      background: #0f0f0f;
      border: 1px solid #1e1e1e;
      border-radius: 12px;
      padding: 32px;
      width: 100%;
      max-width: 480px;
      box-shadow: 0 4px 32px rgba(0, 0, 0, 0.6);
    }

    /* Header */
    .card-header {
      display: flex;
      align-items: center;
      gap: 16px;
      margin-bottom: 20px;
    }

    .avatar {
      width: 56px;
      height: 56px;
      border-radius: 50%;
      border: 2px solid #27a9e1;
      object-fit: cover;
      flex-shrink: 0;
    }

    .card-header-text {
      display: flex;
      flex-direction: column;
      gap: 3px;
    }

    .card-name {
      font-size: 18px;
      font-weight: 600;
      color: #ffffff;
      line-height: 1.2;
    }

    .card-role {
      font-size: 12px;
      color: #888888;
    }

    .divider {
      height: 1px;
      background: #27a9e1;
      opacity: 0.6;
      border: none;
      margin-bottom: 20px;
    }

    /* Bio */
    .bio {
      line-height: 1.7;
      margin-bottom: 20px;
      color: #cccccc;
    }

    /* Social icons */
    .social {
      display: flex;
      justify-content: center;
      gap: 12px;
      list-style: none;
      margin-bottom: 24px;
    }

    .social a {
      display: block;
      opacity: 0.8;
      transition: opacity 0.15s;
    }

    .social a:hover {
      opacity: 1;
    }

    /* Presentations */
    .section-label {
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 0.1em;
      color: #555555;
      margin-bottom: 10px;
    }

    .presentations {
      list-style: none;
      display: flex;
      flex-direction: column;
      gap: 6px;
      margin-bottom: 28px;
    }

    .presentations a,
    .presentations a:visited {
      color: #27a9e1;
      text-decoration: none;
    }

    .presentations a:hover {
      color: #ffffff;
    }

    /* Footer */
    .card-footer {
      text-align: center;
      font-size: 11px;
      color: rgba(255, 255, 255, 0.4);
    }

    /* Mobile */
    @media (max-width: 600px) {
      body {
        padding: 0;
        align-items: flex-start;
      }

      .card {
        border-radius: 0;
        border-left: none;
        border-right: none;
        min-height: 100vh;
      }
    }
  </style>
</head>
<body>
  <div class="bg" aria-hidden="true"></div>

  <div class="card">
    <div class="card-header">
      <img class="avatar" src="images/profile.jpg" alt="Sajnikanth Suriyanarayanan" />
      <div class="card-header-text">
        <div class="card-name">Sajnikanth Suriyanarayanan</div>
        <div class="card-role">Engineering Manager &middot; Amsterdam</div>
      </div>
    </div>

    <hr class="divider" />

    <p class="bio">
      I'm Sajnikanth, a Coastal Geoscientist who wandered into the world of tech, Python, and people.
      I've lived and worked across India, Germany, China, Singapore, and now call The Netherlands home.
      Along the way, I've led teams, automated a few things, and helped build better workplaces.
      I'm also an LVV-registervertrouwenspersoon&reg;; trusted person you can talk to when things don't feel right.
      Always up for meaningful conversations (or coffee).
    </p>

    <ul class="social">
      <li><a href="mailto:mail@sajnikanth.com" target="_blank"><img src="images/email.png" height="48" width="48" alt="email" title="email" /></a></li>
      <li><a href="https://linkedin.com/in/sajnikanth" target="_blank"><img src="images/linkedin.png" height="48" width="48" alt="linkedin" title="linkedin" /></a></li>
      <li><a href="https://goodreads.com/sajnikanth" target="_blank"><img src="images/goodreads.png" height="48" width="48" alt="goodreads" title="goodreads" /></a></li>
      <li><a href="https://github.com/sajnikanth" target="_blank"><img src="images/github.png" height="48" width="48" alt="github" title="github" /></a></li>
    </ul>

    <p class="section-label">Presentations</p>
    <ul class="presentations">
      <li><a href="http://www.youtube.com/watch?v=2ggWbGLkBPk#" target="_blank">Python for black-box testers</a> &ndash; <a href="http://www.slideshare.net/sajnikanth/python-for-blackbox-testers-22923764" target="_blank">slides</a></li>
      <li><a href="http://www.slideshare.net/sajnikanth/introduction-to-holmium" target="_blank">Introduction to holmium</a> &ndash; <a href="http://lifeinvistaprint.com/techblog/unit-testing-holmium-page-objects/" target="_blank">blog</a></li>
      <li><a href="http://www.slideshare.net/sajnikanth/qa-to-sous-chef" target="_blank">QA to sous-Chef</a></li>
      <li><a href="http://www.slideshare.net/sajnikanth/introduction-to-saucelabs" target="_blank">Introduction to SauceLabs</a></li>
    </ul>

    <div class="card-footer">
      &copy; Sajnikanth Suriyanarayanan,
      <script>document.write(new Date().getFullYear());</script>
    </div>
  </div>

  <script>
    (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
    (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
    m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
    })(window,document,'script','//www.google-analytics.com/analytics.js','ga');
    ga('create', 'UA-23959099-1', 'auto');
    ga('send', 'pageview');
  </script>
</body>
</html>
```

- [ ] **Step 3: Open in browser to verify**

```bash
open /Users/ssuriyanarayanan/Library/CloudStorage/Dropbox/repo/domains/sajnikanth.com/index.html
```

Check:
- Blurred dark background photo visible
- Dark card centered on the page
- Circular profile photo next to name
- Blue divider line
- Bio text readable
- 4 social icons present and centered
- Presentations links visible in blue
- Mobile: resize browser to < 600px, card should fill full width

- [ ] **Step 4: Commit**

```bash
cd /Users/ssuriyanarayanan/Library/CloudStorage/Dropbox/repo/domains/sajnikanth.com
git add index.html
git commit -m "Redesign: dark card layout, profile photo, system-ui font, HTML5"
```

---

### Task 4: Add .superpowers to .gitignore

**Files:**
- Modify: `.gitignore` (create if it doesn't exist)

- [ ] **Step 1: Check if .gitignore exists**

```bash
cat /Users/ssuriyanarayanan/Library/CloudStorage/Dropbox/repo/domains/sajnikanth.com/.gitignore 2>/dev/null || echo "no .gitignore"
```

- [ ] **Step 2: Add .superpowers entry**

If `.gitignore` doesn't exist, create it. If it does, append to it. Either way, ensure it contains:

```
.superpowers/
```

- [ ] **Step 3: Commit**

```bash
cd /Users/ssuriyanarayanan/Library/CloudStorage/Dropbox/repo/domains/sajnikanth.com
git add .gitignore
git commit -m "Add .gitignore with .superpowers/"
```
