<p align="center"><img src="assets/icon-192.png" width="96" alt="Guardian logo"></p>

# Guardian · website

Public website for **Guardian**, a private AI command center that runs on your own computer.

**Live site:** https://sokul-13.github.io/guardian-web/

| Page | Link |
|---|---|
| Home | https://sokul-13.github.io/guardian-web/ |
| Privacy policy | https://sokul-13.github.io/guardian-web/privacy.html |
| Terms of service | https://sokul-13.github.io/guardian-web/terms.html |
| Google setup guide | https://sokul-13.github.io/guardian-web/GOOGLE.html |

The Guardian app itself is in private beta. To request access, [open an issue](https://github.com/SoKul-13/guardian-web/issues/new?title=Access%20request).

This site is static HTML served by GitHub Pages (Settings → Pages → Deploy from branch `main`, folder `/`).

## Updating the site

```bash
cd ~/Documents/GitHub/guardian-web
git add -A
git commit -m "Update the website"
git push                     # live in 1–2 minutes
gh api repos/SoKul-13/guardian-web/pages/builds/latest -q .status   # "built" when it's live
```

This repo is public and contains only the website: no app code, no personal data, no secrets.
The Guardian app (`SoKul-13/guardian`) and personal backups (`SoKul-13/guardian-data`) are separate private repos.
