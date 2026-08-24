# TopKid Dashboard — setup (about 15 minutes)

You already have a GitHub account signed in on this Mac: **TopKidEvents**.
So there's no account to create — skip straight to Step 1.

Two repos, on purpose:

| Repo | Visibility | Holds |
|---|---|---|
| `topkid-dashboard` | **Public** | the page itself — HTML, icons. No business data. |
| `topkid-dashboard-data` | **Private** | `data.json` — every school, contact, note, dollar figure. |

The page has to be public because GitHub Pages only serves public repos on the
free plan. That's fine: the page is an empty shell until it's given a token.
Anyone who finds the URL sees a dashboard with nothing in it.
(If you'd rather the page were private too, that's GitHub Pro at $4/month —
tell me and I'll switch it.)

---

## Step 1 — create the two repos

Run this in Terminal from the `TopKid Business Folder`:

```bash
cd "/Users/topkid/TopKid Business Folder/TopKid Dashboard Site" && gh repo create topkid-dashboard --public --source=. --remote=origin --push && gh repo create topkid-dashboard-data --private --add-readme
```

## Step 2 — turn on GitHub Pages

```bash
gh api -X POST repos/TopKidEvents/topkid-dashboard/pages -f "source[branch]=main" -f "source[path]=/"
```

Give it a minute, then your dashboard is live at:

**https://topkidevents.github.io/topkid-dashboard/**

## Step 3 — make an access token

This part is yours — it's a credential, so nobody else should create or handle it.

1. Go to <https://github.com/settings/personal-access-tokens/new>
2. **Token name:** `topkid-dashboard`
3. **Expiration:** 1 year
4. **Repository access:** *Only select repositories* → pick **`topkid-dashboard-data`** only
5. **Permissions:** expand *Repository permissions* → set **Contents** to **Read and write**.
   Leave everything else alone.
6. Click **Generate token** and copy it. You only get to see it once.

## Step 4 — connect the dashboard

1. Open **https://topkidevents.github.io/topkid-dashboard/**
2. **Data & Backup → Set up sync**
3. Fill in:
   - GitHub account: `TopKidEvents`
   - Repo name: `topkid-dashboard-data`
   - File: `data.json`
   - Branch: `main`
   - Access token: paste it
4. **Save & sync.** The sidebar should show a green ● Synced.

## Step 5 — move your existing data up

Only if you've already entered real data locally.

1. Open your local copy, **Data & Backup → Export JSON**
2. On the Pages URL, **Import JSON**, pick that file
3. It pushes to the private repo within a few seconds

## Step 6 — put it on your phone

1. Open **https://topkidevents.github.io/topkid-dashboard/** in Safari
2. Share button → **Add to Home Screen** → it installs with the TopKid icon
3. Open it, **Data & Backup → Set up sync**, same details, paste the same token

Both devices now read and write the same file. Edit on the phone at a PTA
meeting, and it's on the Mac when you get home.

---

## How it behaves

- **Every save is a commit.** Data & Backup → *Version history* lists them.
  *Restore* brings any past version back **as a new commit** — nothing is erased,
  so restoring is itself undoable.
- **Two devices edited at once?** You get a conflict box showing both, with
  timestamps and record counts. Nothing is auto-discarded, and whichever you
  don't pick stays in the history.
- **Offline?** It keeps working from local storage and pushes when you're back.
- **Belt and braces:** on the Mac you can *also* connect a local `TopKid-Data.json`
  (Data & Backup → Data file) so there's a copy on disk independent of GitHub.

## Token safety

- Scoped to the data repo alone. It cannot touch anything else in your account.
- Stored per-device, and stripped out of the data before every push — it is
  never committed to the repo. (Verified by test.)
- Lost your phone? <https://github.com/settings/tokens> → delete the token.
  Then make a new one and re-enter it on your remaining devices.
- The `.gitignore` in this folder blocks `data.json` from ever being committed
  to the *public* page repo by accident.

## Updating the page later

```bash
cd "/Users/topkid/TopKid Business Folder/TopKid Dashboard Site" && git add -A && git commit -m "Dashboard update" && git push
```

Pages redeploys in under a minute. Your data is untouched — it lives in the
other repo.
