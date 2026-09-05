# shoebill-site

The marketing, privacy and support pages for the Shoebill iPhone app, served from
GitHub Pages at `https://shoebill.nathanlangley.dev`.

Plain HTML and one stylesheet. No build step, no dependencies. Open
`index.html` in a browser to preview it locally.

```
index.html     the marketing page
privacy.html   the privacy policy (App Store Connect: Privacy Policy URL)
support.html   contact, reporting, blocking (App Store Connect: Support URL)
style.css      the single shared stylesheet
img/           app icon, favicon, and four real device screenshots
CNAME          the custom domain, required by GitHub Pages
.nojekyll      stops Pages running Jekyll over the folder
robots.txt     allows all crawlers
sitemap.xml    the three pages
```

## Before you publish

Replace the TestFlight placeholder. The link
`https://testflight.apple.com/join/REPLACE` appears in `index.html`,
`privacy.html` and `support.html`. Find and replace it in all three with the
real public beta link from App Store Connect.

## Deploying it

1. **Create a public repo on GitHub.** Suggested name: `ninjahawk/shoebill-site`.
   It has to be public unless the account has GitHub Pro, because Pages on a
   private repo is a paid feature.

2. **Push this folder to it.**

   ```
   cd C:\Users\jedin\Desktop\shoebill-site
   git init
   git add -A
   git commit -m "Shoebill site"
   git branch -M main
   git remote add origin https://github.com/ninjahawk/shoebill-site.git
   git push -u origin main
   ```

3. **Turn Pages on.** Repo, Settings, Pages. Under "Build and deployment" set
   Source to "Deploy from a branch", Branch to `main`, folder to `/ (root)`,
   then Save. The first deploy takes a minute or two.

4. **Point the domain at it.** In the DNS for `nathanlangley.dev`, add:

   | Type | Name | Value |
   |---|---|---|
   | CNAME | `shoebill` | `ninjahawk.github.io` |

   Use `ninjahawk.github.io`, not the repo name, and no trailing content after
   it. Some DNS panels want a trailing dot (`ninjahawk.github.io.`); either
   works if the panel adds it for you.

5. **Confirm the custom domain in GitHub.** Settings, Pages, Custom domain:
   enter `shoebill.nathanlangley.dev` and Save. The `CNAME` file in this repo
   already holds that value, so it should populate itself; if GitHub reports
   "domain does not resolve", wait for DNS to propagate (usually minutes, up to
   an hour) and press Save again.

6. **Wait for the certificate.** Once the DNS check passes, GitHub issues a
   Let's Encrypt certificate on its own — normally within 15 minutes, sometimes
   up to 24 hours. When it is ready, tick **Enforce HTTPS** on the same page.
   Do not tick it before then; it is greyed out until the certificate exists.

7. **The three URLs**, once HTTPS is enforced:

   - `https://shoebill.nathanlangley.dev/` — marketing (App Store Connect: Marketing URL)
   - `https://shoebill.nathanlangley.dev/privacy.html` — Privacy Policy URL, required
   - `https://shoebill.nathanlangley.dev/support.html` — Support URL, required

## Updating it

Edit the files, commit, push. Pages redeploys in about a minute. There is
nothing to rebuild.

## Assets

Every image in `img/` is real: `icon.png` is the shipping app icon, and the four
screenshots are unretouched captures from the app running on an iPhone 16 Pro
Max, downscaled for the web. Nothing on this site is generated, stock or
illustrated.
