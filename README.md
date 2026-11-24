# elena_portfolio

Elena Dobrowney's portfolio, live at **https://elena.dobrowney.com**.

- `public/`: the website (plain static files). This folder is the nginx web root, and nothing outside it is served.
- `deploy/nginx/elena.dobrowney.com.conf`: the nginx vhost.

## Deploying

Push to `main`. Within about 5 minutes the VPS pulls the change and the site is live. There is no build step.

The VPS clone at `/srv/sites/elena_portfolio` is kept up to date by the shared **site-sync** timer. Its script, units, repo list and the full one-time setup runbook live in the [`tristan_portfolio`](https://github.com/DobrowneyT/tristan_portfolio) repo under `deploy/site-sync/` and its README.

Local preview: `python3 -m http.server -d public 8000`, then open http://localhost:8000.

## One-time VPS setup for this site

After site-sync is set up (see the tristan_portfolio README):

```bash
sudo -u sitesync git clone https://github.com/DobrowneyT/elena_portfolio.git /srv/sites/elena_portfolio
grep -q elena_portfolio /etc/site-sync/repos.list || echo /srv/sites/elena_portfolio | sudo tee -a /etc/site-sync/repos.list

sudo certbot certonly --nginx --cert-name elena.dobrowney.com -d elena.dobrowney.com
sudo cp /srv/sites/elena_portfolio/deploy/nginx/elena.dobrowney.com.conf /etc/nginx/sites-available/elena.dobrowney.com
sudo ln -s /etc/nginx/sites-available/elena.dobrowney.com /etc/nginx/sites-enabled/
sudo nginx -t && sudo systemctl reload nginx
curl -sI https://elena.dobrowney.com | head -1     # HTTP/2 200
```
