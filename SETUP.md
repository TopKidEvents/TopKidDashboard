# TopKid Dashboard — what's done, what's left

## ✅ Already done

| | |
|---|---|
| **Your dashboard is live** | <https://topkidevents.github.io/TopKidDashboard/> |
| Page repo (public) | `TopKidEvents/TopKidDashboard` — HTML, icons, this guide |
| Data repo (private) | `TopKidEvents/TopKidDashboard-Data` — will hold `data.json` |
| GitHub Pages | enabled, built, HTTPS enforced |

**The public page holds none of your business data.** Before pushing it I stripped
the built-in starter content out — no school names, no revenue figures, no camp
venue. Verified on the live site: 0 schools and 0 goals in the page source. All of
that now travels in your private data file instead.

Your starter content wasn't thrown away — it's in
`TopKid Business Folder/TopKid-Starter-Data.json` (12 Columbus-area target
schools, the goals, the camp weeks, the values). Import it in Step 3 if you want
it; skip it if you'd rather start clean.

---

## Step 1 — make an access token  *(5 min, only you can do this)*

This is a credential, so it's yours alone to create. I won't handle it.

1. Go to <https://github.com/settings/personal-access-tokens/new>
2. **Token name:** `topkid-dashboard`
3. **Expiration:** 1 year
4. **Repository access:** *Only select repositories* → pick **`TopKidDashboard-Data`**
   — the private one. Not the public page repo.
5. **Permissions:** expand *Repository permissions* → set **Contents** to
   **Read and write**. Leave everything else alone.
6. **Generate token**, then copy it. GitHub shows it once.

## Step 2 — get your existing data out of the old copy

Skip if you haven't entered anything real yet.

Open your **local** dashboard the way you have been, then
**Data & Backup → Export JSON**. Keep that file handy.

> Why: browser storage is tied to the exact address. Anything you typed at the
> old address isn't visible at the new one — it's parked, not lost, and this
> moves it across.

## Step 3 — load your data into the live dashboard

Open <https://topkidevents.github.io/TopKidDashboard/> and go to
**Data & Backup → Import JSON**. Pick either:

- the file you exported in Step 2 (your real data), **or**
- `TopKid-Starter-Data.json` from your business folder (the starter content)

**Do this before Step 4.** Importing first means your real data is what gets
pushed up, rather than an empty dashboard.

## Step 4 — turn on sync

Still on the live dashboard: **Data & Backup → Set up sync**

| Field | Value |
|---|---|
| GitHub account | `TopKidEvents` |
| Repo name | `TopKidDashboard-Data` |
| File in the repo | `data.json` |
| Branch | `main` |
| Access token | paste the token from Step 1 |

**Save & sync.** The sidebar should show a green **● Synced**. Check
<https://github.com/TopKidEvents/TopKidDashboard-Data> — `data.json` will be there.

## Step 5 — put it on your phone

1. Open <https://topkidevents.github.io/TopKidDashboard/> in Safari
2. Share → **Add to Home Screen** — it installs with the TopKid icon
3. Open it → **Data & Backup → Set up sync** → same five fields, same token

Both devices now read and write the same file. Log outreach at a PTA meeting on
your phone; it's on the Mac when you get home.

---

## How it behaves

- **Every save is a commit.** *Data & Backup → Version history* lists them.
  *Restore* brings a past version back **as a new commit**, so restoring is
  itself undoable and nothing is ever erased.
- **Two devices edited at once?** You get a box showing both, with timestamps and
  record counts, and you choose. Nothing is auto-discarded; the version you
  don't pick stays in the history.
- **Offline?** Keeps working locally and pushes when you're back.
- **Extra belt on the Mac:** *Data & Backup → Data file* also writes a plain
  `TopKid-Data.json` to your business folder, independent of GitHub.

## Token safety

- Scoped to the data repo alone — it cannot touch anything else in your account.
- Stored per-device and stripped from the payload before every push, so it is
  never committed. Verified by test.
- Lost your phone? <https://github.com/settings/tokens> → delete the token, then
  make a new one and re-enter it on your other devices.
- If you ever paste real data into the **public** repo by accident, tell me —
  it has to be scrubbed from git history, not just deleted.

## Updating the page later

```bash
cd "/Users/topkid/TopKid Business Folder/TopKid Dashboard Site" && git add -A && git commit -m "Dashboard update" && git push
```

Pages redeploys in under a minute. Your data is untouched — it lives in the
other repo.
