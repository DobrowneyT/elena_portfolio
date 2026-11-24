# elena_portfolio

Elena Dobrowney's portfolio, live at **https://elena.dobrowney.com**.

- `public/`: the website (plain static files). This folder is the nginx web root, and nothing outside it is served.
- `deploy/nginx/elena.dobrowney.com.conf`: the nginx vhost.

## Deploying

Push to `main`. Within about 5 minutes the VPS pulls the change and the site is live. There is no build step.

The VPS clone at `/srv/sites/elena_portfolio` is kept up to date by the shared **site-sync** timer. Its script, units, repo list and the full one-time setup runbook live in the [`tristan_portfolio`](https://github.com/DobrowneyT/tristan_portfolio) repo under `deploy/site-sync/` and its README.

Local preview: `python3 -m http.server -d public 8000`, then open http://localhost:8000.

## One-time VPS setup for this site

Covered in full, together with the shared site-sync timer, in the [tristan_portfolio README](https://github.com/DobrowneyT/tristan_portfolio#one-time-vps-setup). In short: clone to `/srv/sites/elena_portfolio` as `ubuntu`, get a certificate with `certbot certonly`, install `deploy/nginx/elena.dobrowney.com.conf`, and make sure `/srv/sites/elena_portfolio` is in `/etc/site-sync/repos.list`.
