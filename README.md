# Modularization R&R Dashboard

Interactive HTML dashboard for GS E&C Modularization Project R&R documentation.

## 🔐 Credentials

| ID | Password |
|---|---|
| `gs-modul` | *(shared separately)* |

> ⚠ Password is NOT stored in this README. It has been shared via secure channel.
> See **"Changing credentials"** below to rotate.

## 📄 Features

- **Page 1** — ITC 기준 통합 R&R 매트릭스 (Proposal + Execution + Shipment)
- **Page 2** — ModuleWorkFlow (TBU) 2025 · 71개 Activity, 16개 Discipline
- **Page 3** — Workflow Simulation (SPMT + Barge 해상 운송 애니메이션)
- **Dashboard** — Page 1/2 상단 실시간 통계 + 클릭 연동
- **Interactive** — 노드 드래그, midpoint 곡선 조정, bridge 오버패스

## 🛡 Security

This is a **client-side only** protected document. It blocks:

- ✅ Text selection / drag
- ✅ Right-click menu
- ✅ Copy / Cut / Paste (Ctrl+C/X/V)
- ✅ Save page (Ctrl+S) / View source (Ctrl+U)
- ✅ Print (Ctrl+P) + @media print blocked
- ✅ DevTools shortcuts (F12, Ctrl+Shift+I/J/C)
- ✅ Image dragging
- ✅ Basic DevTools detection (blur + warning)
- ✅ Blur shield when window loses focus
- ✅ SHA-256 based login with session persistence

### ⚠ Security limitations (IMPORTANT)

Because this runs in a static HTML file (GitHub Pages is a static host):

- ❌ **Screenshot tools, OS PrintScreen, phone cameras cannot be blocked**
- ❌ A determined user with DevTools CAN bypass client-side auth
- ❌ The SHA-256 hashes are visible in the HTML source (via `view-source:` or raw GitHub)
- ❌ Anyone with the repo URL + password can access

**For real confidential documents, use a private GitHub repo + GitHub Pages Enterprise, or better: a real server with server-side authentication (e.g. Cloudflare Access, nginx basic auth, Auth0).**

## 🔑 Changing credentials

1. Open the file in Chrome/Edge
2. Press F12 → Console tab
3. Run:
   ```js
   crypto.subtle.digest('SHA-256', new TextEncoder().encode('myuser:mypass'))
     .then(b => console.log(Array.from(new Uint8Array(b))
       .map(x => x.toString(16).padStart(2, '0')).join('')));
   ```
4. Copy the printed hex string
5. Open `Modularization_RnR_ITC_by_Discipline.html`, find:
   ```js
   window.AUTH_HASHES = [
     '2bb33a9e64...',  // admin:modul2026
   ];
   ```
6. Replace with your hash(es). Multiple entries allowed for multiple accounts.

## 🚀 Publishing to GitHub Pages

```bash
# 1. Create a NEW private repo on github.com (recommended for confidential docs)
#    - Go to github.com → New repository
#    - Name it, e.g. "modularization-rnr-dashboard"
#    - Set to PRIVATE
#    - Do NOT initialize with README (we have one)

# 2. From the project folder:
cd "E:/공유폴더/CoworkProjects/참조 Modularization 자료"
git init
git add Modularization_RnR_ITC_by_Discipline.html
git add module_transport_bg.png
git add README.md
git add .gitignore
git commit -m "Initial: Modularization R&R Dashboard with auth + content protection"

# 3. Connect to remote and push
git branch -M main
git remote add origin https://github.com/<YOUR_USERNAME>/modularization-rnr-dashboard.git
git push -u origin main

# 4. Enable GitHub Pages
#    - Repo → Settings → Pages
#    - Source: "Deploy from a branch"
#    - Branch: main / (root)
#    - Save
#    - Wait ~1 minute, URL: https://<YOUR_USERNAME>.github.io/modularization-rnr-dashboard/Modularization_RnR_ITC_by_Discipline.html

# 5. (Optional but recommended) Rename to index.html for cleaner URL
git mv Modularization_RnR_ITC_by_Discipline.html index.html
git commit -m "Rename to index.html"
git push
# Now accessible at: https://<YOUR_USERNAME>.github.io/modularization-rnr-dashboard/
```

## 🔒 Private repo + Pages note

- **Free GitHub accounts**: Pages on private repos require GitHub Pro/Team/Enterprise
- **Public repo alternative**: anyone who finds the URL + guesses credentials can read the page
- **Best option**: Use GitHub Enterprise + Pages with IP allowlist, or Cloudflare Access in front of a private bucket

## 📁 Files

| File | Purpose |
|---|---|
| `Modularization_RnR_ITC_by_Discipline.html` | Main dashboard (self-contained) |
| `module_transport_bg.png` | Background image for Page 3 (Korea→Yanbu route) |
| `README.md` | This file |
| `.gitignore` | Excludes scratch files, Python scripts |

## License

Internal use only. GS E&C © 2026
