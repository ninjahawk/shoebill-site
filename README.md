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
wiki/          the knowledge wiki, Markdown, built by Jekyll
_config.yml    Jekyll + Just the Docs configuration for the wiki
_sass/         the Just the Docs colour scheme that matches style.css
CNAME          the custom domain, required by GitHub Pages
robots.txt     allows all crawlers
sitemap.xml    the pages
```

## How the wiki is built

The three HTML pages above are plain files with no front matter, so Jekyll
copies them through untouched. The wiki is different: `wiki/*.md` is Markdown
with Just the Docs front matter, and GitHub Pages builds it.

- `_config.yml` sets `remote_theme: just-the-docs/just-the-docs` with the
  `jekyll-remote-theme` plugin, `search_enabled: true`, `color_scheme: shoebill`,
  an `aux_links` entry back to the site root, and the footer contact line.
- `_sass/color_schemes/shoebill.scss` imports the theme's dark scheme and then
  restates every colour with the values from `style.css`.
- **There must be no `.nojekyll` file.** Its presence stops Pages running Jekyll
  at all, which would serve the wiki as raw Markdown. It has been removed.
- Nothing here can be built or previewed on a Windows machine without Ruby and
  Jekyll installed. The build that matters is GitHub's.

**Where to check the build.** After a push, open the repo's **Actions** tab and
look at the most recent **"pages build and deployment"** run. Green means the
site rebuilt; red means Jekyll failed, and the log names the file and line.
A Jekyll failure takes the whole site down, not just the wiki, so check it after
any change to `_config.yml`, `_sass/` or a page's front matter.

To add a wiki page: create `wiki/NAME.md`, give it front matter with
`layout: default`, a `title`, and a `nav_order`, and add it to `sitemap.xml`.

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
   - `https://shoebill.nathanlangley.dev/wiki/` — the wiki

## Updating it

Edit the files, commit, push. Pages redeploys in about a minute. The HTML
pages need no build; the wiki is rebuilt by Jekyll on GitHub, so watch the
Actions tab if a wiki page or the config changed.

## Assets

Every image in `img/` is real: `icon.png` is the shipping app icon, and the four
screenshots are unretouched captures from the app running on an iPhone 16 Pro
Max, downscaled for the web. Nothing on this site is generated, stock or
illustrated.
