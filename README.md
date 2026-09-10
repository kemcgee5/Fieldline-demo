# Fieldline — deploy this to a live URL

Two versions of the dashboard are in this folder:

- `index.html` — the static demo, exactly what you've already seen.
- `index-supabase.html` — the same page, wired to read its "Today's
  Schedule" table from a live Supabase database instead of hard-coded data.
  It falls back to the static demo automatically until you fill in real
  Supabase credentials, so it's safe to deploy either way.

The full walkthrough — Supabase, GitHub, and Vercel, in order, with the
exact SQL to run — is in the "Shipping Fieldline" guide Claude published
as an Artifact. The short version is below.

## One-time setup (about 20 minutes with Supabase, 10 without)

**If you want live data (recommended for the trial run):**
1. Create a free Supabase project at https://supabase.com/dashboard/sign-up,
   run the table-creation SQL from the guide, load in the sample rows, and
   copy your Project URL + anon public key from Project Settings → API.
2. Open `index-supabase.html` in a text editor, paste those two values into
   the `SUPABASE_URL` / `SUPABASE_ANON_KEY` lines near the top of the
   script, save, and rename it to `index.html` (replacing the static one).

**If you just want the demo live, skip straight to GitHub:**

3. **Create a GitHub account** at https://github.com/join if you don't
   already have one. It's free.
4. **Create a new repository**
   - Click the "+" in the top-right corner of GitHub → "New repository"
   - Name it something like `fieldline-demo`
   - Leave it "Public" or set it to "Private" — either works for this
   - Click "Create repository"
5. **Upload these files**
   - On the new repo's page, click "uploading an existing file"
   - Drag in `index.html` (and this `README.md` if you want) from this folder
   - Click "Commit changes"
6. **Create a Vercel account** at https://vercel.com/signup
   - Choose "Continue with GitHub" — this uses your GitHub login instead of
     making you set a new password, and it's what lets Vercel see your repos
7. **Import the project**
   - From your Vercel dashboard, click "Add New" → "Project"
   - Find `fieldline-demo` in the list and click "Import"
   - Leave every setting as its default (no framework, no build command —
     it isn't needed for a plain HTML file) and click "Deploy"
8. Vercel gives you a live URL (something like `fieldline-demo.vercel.app`)
   within about 30 seconds. That's a real, shareable link — no more sending
   people a file to download and open. If you wired up Supabase, the badge
   next to "Fieldline" will read "Live · Supabase" instead of "Demo."

## Making updates later

Any time you (or Claude) change `index.html` and re-upload it to the same
GitHub repo, Vercel automatically rebuilds and redeploys the live site
within a minute or two — no extra steps on the Vercel side.

## If you'd rather not use the GitHub website

If you ever install `git` on your computer, the same result comes from:

```
git init
git add index.html README.md
git commit -m "Fieldline demo"
git branch -M main
git remote add origin <your-empty-repo-URL-from-GitHub>
git push -u origin main
```

Vercel picks up changes the same way either way — it's watching the
repository, not how the files got there.
