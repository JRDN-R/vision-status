# Vision Status

Private owner dashboard for Vision and Vortex at https://jrdn-r.github.io/vision-status/.

The horizontal module bar opens one view at a time:

- **Overview:** compact account, activity, transcription, Gemini, and Vortex totals.
- **Vortex:** retained jobs, queue status, ready downloads, formats, file sizes, and expiration.
- **Transcriptions:** local and Gemini transcription activity, filtered on the server before pagination.
- **Gemini:** existing account approvals, request usage, tokens, and estimated costs.
- **Logins:** account names/email addresses, Google or email/password sign-in methods, observed apps, and session sightings.
- **Activity:** the complete retained event timeline.

The account selector scopes activity, Gemini usage, and Vortex jobs. Gemini access approvals remain global administrative controls. Tabs support arrow keys, Home, and End; the tab bar scrolls horizontally on phones.

## Companion PC update

This page is mirrored in `JRDN-R/vision/activity.html`. Deploy the matching Vision changes to `vision-pc/activity_dashboard.py`, `audit_logs.py`, `server.py`, and `vortex.py` using the normal `Setup-Vision-PC.ps1 -Action Update` workflow after merging the companion PR. Updating only this GitHub Pages repository does not update the PC service. The dashboard reports missing Vortex support without hiding existing Vision activity.

The existing owner allowlist is required for every admin endpoint. The Vortex report uses existing retained job records, so it does not start with an empty history after updating. Provider and app observations begin when accounts next contact the updated PC; older unrecorded providers are labeled **Not recorded**. Shared account sessions are counted once, even when used in both apps.

Vortex reports contain operational metadata only. They exclude media URLs, search terms, titles, filenames, download tickets, and extractor diagnostics. A ready job means a file was prepared on the server, not that the person saved it on their device. Files expire after five days; deleted jobs are excluded from retained totals.

## Preview and verification

Open `?demo=1` for an explicitly labeled sample preview that never contacts the PC or Firebase. Approvals are disabled in this mode.

```sh
python -m pip install playwright
python -m playwright install chromium
python tests/activity_browser_smoke.py
```

The browser regression uses fake authentication and API responses to check tabs, account scoping, approvals, token/account races, sign-out clearing, missing PC support, and mobile/desktop layouts. It does not make real account changes or media downloads. Set `CHROMIUM_PATH` to use an already installed Chromium binary.
