# Droid Agent — GitHub Pages site for app-ads.txt verification

This folder is the content of the GitHub Pages site that proves you own the
"Droid Agent" Android app to AdMob (app-ads.txt ownership verification).

## Why this is needed

The "Developer website" currently set in the Play Console for Droid Agent is:

    https://github.com/MohamedM-Haroon/PRIVACY_POLICY/blob/main/Apps/droid%20agent/PRIVACY_POLICY.md

Google's app-ads.txt crawler uses only the **hostname** of the developer
website from the store listing. From that URL the hostname is `github.com`,
so AdMob looks for:

    https://github.com/app-ads.txt
    http://github.com/app-ads.txt

You can never publish a file at the root of `github.com`, so verification
always fails with "details don't match the information in your AdMob account".

The fix: publish `app-ads.txt` at the root of a domain you control and put
**that** domain in the Play Console developer website field.

## Step 1 — create the Pages repo (repo name is exact)

On GitHub, create a new repository named exactly:

    mohamedm-haroon.github.io

GitHub special-cases that name and serves it at `https://mohamedm-haroon.github.io/`.
(Any other repo name publishes under a path, and the crawler only checks the
domain root, so a repo named `PRIVACY_POLICY` will NOT work.)

Upload the contents of this folder to the root of that repo:

    app-ads.txt
    index.html

`app-ads.txt` must contain exactly one line:

    google.com, pub-6676511719467184, DIRECT, f08c47fec0942fa0

## Step 2 — turn on GitHub Pages

Repo -> Settings -> Pages -> Build and deployment -> Source: **Deploy from a
branch** -> branch `main`, folder `/ (root)` -> Save.
Wait for the deploy to finish (usually a minute or two).

## Step 3 — check the file is live

Open in a browser:

    https://mohamedm-haroon.github.io/app-ads.txt

It must show the plain text line. If you get a 404, Pages is not on yet (or the
repo name is wrong). If you get an HTML page, the file is not at the repo root.

## Step 4 — point the Play Store at it

Play Console -> your app -> Grow users -> Store presence -> Store settings ->
Store listing contact details -> **Developer website**:

    https://mohamedm-haroon.github.io

Remove the `github.com/.../blob/...` URL from that field. Save and publish the
store listing change (it can take a few hours to go live; allow up to 24h for
Google's crawler to notice).

## Step 5 — re-run the check in AdMob

1. AdMob -> Apps -> View all apps -> app-ads.txt -> expand "Droid Agent" ->
   **Check for updates**
2. AdMob -> App settings -> **Verify app** -> Check for updates
3. The app readiness review follows (policy check of the app itself).

## Notes

- Use the apex domain, no `www.`, no path, and `https://`.
- If it still fails, confirm the file returns plain text (not HTML) over both
  http and https, and that the domain in Play matches character for character.
- Alternative to GitHub Pages: Firebase Hosting (Google's own suggestion in the
  app-ads.txt guide) on the free `web.app` subdomain, or a cheap custom domain
  pointed at GitHub Pages / Cloudflare Pages.
