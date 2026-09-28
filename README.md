# Fast Lane

Personal fasting, weigh-in and workout tracker with a points-based weekly score.

- **App (this repo, public):** `index.html`, `manifest.json`, `icon-512.png`, served by GitHub Pages.
- **Data (separate private repo):** a single `data.json`, written by the app through the GitHub API.
  This repo never holds any personal data.

## Setup

1. Create a **private** repo named `fast-lane-data`, and tick "Add a README file" when you create it.
2. Create a fine-grained personal access token:
   GitHub → Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token.
   - Repository access: *Only select repositories* → `fast-lane-data`
   - Permissions → Repository permissions → **Contents: Read and write**
3. Enable GitHub Pages on this repo: Settings → Pages → Deploy from a branch → `main` / root.
4. Open the Pages URL on each device, go to **Settings → GitHub sync**, and enter your username,
   `fast-lane-data`, and the token. The token is stored only on that device.

## How syncing works

Every change is saved on the device first, then merged into the latest `data.json` and committed,
so edits from your phone and iPad don't overwrite each other. If you're offline, changes queue up
and upload the next time the app is open with a connection. Each save is a commit, so the repo
history doubles as a full backup.

## data.json shape

```json
{
  "version": 1,
  "days":  { "2026-09-28": { "weight": 212.4, "workouts": [{ "type": "lift", "min": 40, "at": 1790000000000 }],
                             "garmin": { "hrv": 58, "rhr": 52, "sleepScore": 81, "vo2max": 44, "steps": 9120 } } },
  "fasts": { "<id>": { "start": 1790000000000, "end": 1790060000000 } },
  "settings": { "...": "points, weekly target, plan, goals, rewards" }
}
```

`garmin` data is for tracking only and never earns points.
