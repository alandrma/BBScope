# BBScope — Bug Bounty Scope Monitor

A lightweight, single-file HTML dashboard for monitoring bug bounty program scopes across **5 major platforms** in real time. No backend, no build tools, no dependencies — open the file in a browser and you're ready to hunt.

---

## Preview

> Dark-themed dashboard with tab navigation per platform, program cards with expandable scope details, live search, and bounty filters.

---

## Features

- **Live data fetching** — pulls fresh JSON data from [arkadiyt/bounty-targets-data](https://github.com/arkadiyt/bounty-targets-data) on every page load or manual refresh
- **5 platforms in one view** — Bugcrowd, Federacy, Intigriti, YesWeHack, HackerOne
- **Summary dashboard** — total program count per platform and bounty-eligible count at a glance
- **Tab navigation** — switch between platforms with live badge counts
- **Expandable program cards** — view in-scope and out-of-scope targets per program without leaving the page
- **Platform-native fields** — each platform displays its own raw field structure (no normalization)
- **Search** — filter programs by name or scope target in real time
- **Bounty / VDP filter** — quickly isolate paid programs or disclosure-only programs
- **Pagination** — 50 programs per page, handles platforms with thousands of entries
- **Zero dependencies** — pure HTML, CSS, and vanilla JS; fonts loaded from Google Fonts

---

## Supported Platforms & Fields

| Platform | Bounty Field | Status Field | Extra Fields |
|---|---|---|---|
| **Bugcrowd** | `max_payout` | — | `safe_harbor`, `managed_by_bugcrowd`, `allows_disclosure` |
| **Federacy** | `offers_awards` | — | `id` |
| **Intigriti** | `min_bounty`, `max_bounty` (+ currency) | `status` | `confidentiality_level`, `tacRequired`, `twoFactorRequired` |
| **YesWeHack** | `min_bounty`, `max_bounty` | `disabled` | `public`, `managed` |
| **HackerOne** | `offers_bounties` | `submission_state` | `response_efficiency_percentage`, `average_time_to_first_program_response`, `managed_program` |

Scope fields are preserved as-is per platform:
- Bugcrowd / Federacy / YesWeHack → `target`
- Intigriti → `endpoint` + `description` + `impact`
- HackerOne → `asset_identifier` + `max_severity` + `eligible_for_bounty`

---

## Usage

### Option 1 — Open directly in browser

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
open bugbounty-dashboard.html   # macOS
xdg-open bugbounty-dashboard.html   # Linux
```

Or just double-click the file. No server needed.

### Option 2 — Serve locally (recommended for CORS-safe fetching)

```bash
# Python 3
python3 -m http.server 8080

# Then open:
# http://localhost:8080/bugbounty-dashboard.html
```

### Option 3 — GitHub Pages

1. Push the file to your repository
2. Go to **Settings → Pages**
3. Set source to your branch and root `/`
4. Access via `https://<your-username>.github.io/<your-repo>/bugbounty-dashboard.html`

---

## Data Source

All data is fetched from the community-maintained repository:

**[arkadiyt/bounty-targets-data](https://github.com/arkadiyt/bounty-targets-data)**

Raw JSON endpoints used:

```
https://raw.githubusercontent.com/arkadiyt/bounty-targets-data/main/data/bugcrowd_data.json
https://raw.githubusercontent.com/arkadiyt/bounty-targets-data/main/data/federacy_data.json
https://raw.githubusercontent.com/arkadiyt/bounty-targets-data/main/data/intigriti_data.json
https://raw.githubusercontent.com/arkadiyt/bounty-targets-data/main/data/yeswehack_data.json
https://raw.githubusercontent.com/arkadiyt/bounty-targets-data/main/data/hackerone_data.json
```

Data is fetched with `cache: 'no-store'` to ensure you always get the latest version on refresh.

---

## Project Structure

```
.
└── bugbounty-dashboard.html   # Entire app — HTML + CSS + JS in one file
└── README.md
```

---

## Potential Improvements

- [ ] Export filtered scope list to `.txt` / `.csv` for use in recon tooling
- [ ] Keyword highlight in scope targets matching search query
- [ ] Local storage caching to reduce fetch time on revisit
- [ ] Dark/light theme toggle
- [ ] Direct link to program page on click

---

## Disclaimer

This tool is intended for **authorized security research only**. Always verify that you are within scope before testing any target. The author is not responsible for any unauthorized access or misuse of this tool.

---

## License

MIT — do whatever you want, attribution appreciated.
