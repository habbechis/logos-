# FOOTBALL POSTER STUDIO — PROJECT STATE

## CURRENT CHECKPOINT
V3 deployed — Unicode filename bug fixed. All team logos now load correctly.

## CURRENT BRANCH
main

## LATEST COMMIT
57107cc42f4b — fix: use NFD-normalized filenames for team logos (Unicode fix)

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

## LAST COMPLETED TASK
Fixed Unicode normalization bug in team logo filenames:
- GitHub stores filenames in NFD form (decomposed accents)
- Code was using NFC form (composed accents)
- This caused 404 errors for 6 team logos (EST, ESS, CAB, ESM, OB, PSS)
- Fixed by updating TEAMS object to use NFD-normalized filenames
- Verified all 17 team logo URLs now return 200 OK

## CHANGES MADE
| File | Change |
|------|--------|
| index.html | Fixed TEAMS object: replaced NFC filenames with NFD filenames for accented characters (é, É, è, ï) |

## KNOWN ISSUES
- LIGUE 1 logo extraction has slight red tint on edges (acceptable quality)
- Font loading from GitHub raw may fail due to CORS (fallback fonts active)
- Image loading depends on GitHub raw URLs (no local caching beyond session)
- No save/load functionality (state resets on refresh)
- Render deployment may need cache clear to see updates

## NEXT TASK
Verify the deployed Render site renders correctly with all team logos visible. Wait for user feedback.

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
Render: ⏳ PENDING CACHE CLEAR — user may need hard refresh (Ctrl+Shift+R)
Production URL: https://football-poster-studio-v2.onrender.com/

## HANDOFF NOTES
- The project is a single-file HTML app at index.html
- All assets load from https://raw.githubusercontent.com/habbechis/logos-/main/
- CRITICAL: GitHub filenames use NFD Unicode normalization (decomposed accents)
- The getAssetUrl() function uses encodeURIComponent() which handles this correctly
- When adding new teams, ALWAYS verify the actual filename bytes on GitHub
