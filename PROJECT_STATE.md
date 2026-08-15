# FOOTBALL POSTER STUDIO — PROJECT STATE

## CURRENT CHECKPOINT
V3 deployed — Home/away positions fixed to match reference. All team logos load correctly. Render auto-deploys from GitHub.

## CURRENT BRANCH
main

## LATEST COMMIT
5b53a5478c23 — fix: swap home/away positions - home on LEFT, away on RIGHT (matches reference)

## CURRENT WORKING FEATURES
- Single-file HTML application (no build step)
- Canvas-based poster renderer (1080×1350)
- RTL Arabic editor with live preview
- 17 Tunisian teams mapped with real logos from GitHub
- 4 TV channels mapped (selectable in editor, hidden on poster)
- Dynamic match rows (4–8 matches with auto-scaling)
- PNG export via canvas.toDataURL()
- Animated particle background in editor
- Loading overlay with asset preloading
- Add/Delete match cards
- Reset to default data
- Responsive layout (desktop/mobile)
- Real red background image (bg-red.jpg)
- Real LIGUE 1 logo image (ligue1-logo.png)
- Home team on LEFT, Away team on RIGHT (matches reference)

## LAST COMPLETED TASK
Fixed home/away positions in drawMatchRow() to match reference image:
- Home logo and name now on LEFT side of match bar
- Away logo and name now on RIGHT side of match bar
- Previously they were swapped (home on right, away on left)

## CHANGES MADE
| File | Change |
|------|--------|
| index.html | Swapped homeX and awayX positions in drawMatchRow() |

## KNOWN ISSUES
- LIGUE 1 logo extraction has slight red tint on edges (acceptable quality)
- Font loading from GitHub raw may fail due to CORS (fallback fonts active)
- Image loading depends on GitHub raw URLs (no local caching beyond session)
- No save/load functionality (state resets on refresh)
- Browser cache may show old version after updates (use Ctrl+Shift+R or ?v=2)

## NEXT TASK
Wait for user feedback on deployed result. Verify all 4 matches show correct home/away positions.

## IMPORTANT CONSTRAINTS
- Do NOT rebuild the project from scratch
- Do NOT delete or overwrite working files
- Do NOT change existing team/channel mappings
- Do NOT break existing editor functionality
- Do NOT remove the PNG export feature
- Keep all existing logos, fonts, colors and assets
- GitHub repo is source of truth; Render is baseline

## DEPLOYMENT
GitHub: ✅ UP TO DATE — main branch has all changes
Render: ✅ AUTO-DEPLOY ENABLED — updates within 1–3 minutes of GitHub push
Production URL: https://football-poster-studio-v2.onrender.com/

### How Render Deployment Works
1. Push changes to GitHub main branch
2. Render detects the push automatically
3. Render rebuilds and deploys within 1–3 minutes
4. Open site with `?v=2` or `?nocache=1` to bypass browser cache
5. Press Ctrl+Shift+R (or Cmd+Shift+R) for hard refresh

### When is Manual Deploy needed?
| Situation | Need Manual Deploy? |
|-----------|---------------------|
| Normal changes to index.html | ❌ No — wait 2–3 minutes |
| Adding new files | ❌ No — wait 2–3 minutes |
| Render hasn't updated after 10 minutes | ✅ Yes — click Manual Deploy |
| Build error on Render | ✅ Yes — click Manual Deploy |

### How to force cache refresh
- Add `?v=2` or `?nocache=1` to URL
- Press Ctrl+Shift+R (hard refresh)
- Open in Incognito/Private mode
- Clear browser cache completely

## HANDOFF NOTES
- The project is a single-file HTML app at index.html
- All assets load from https://raw.githubusercontent.com/habbechis/logos-/main/
- CRITICAL: GitHub filenames use NFD Unicode normalization (decomposed accents)
- The getAssetUrl() function uses encodeURIComponent() which handles this correctly
- When adding new teams, ALWAYS verify the actual filename bytes on GitHub
- Render auto-deploys from GitHub — no manual action needed for normal updates
