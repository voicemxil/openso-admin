# openso-admin

Deploy repo for the **OpenSO admin webapp** — the AngularJS SPA used to manage shards,
users, hosts, restarts/updates, and client update generation.

This repo holds **no source code**. The admin UI source lives in the main OpenSO repo at
[`TSOClient/FSO.Server/Admin`](https://github.com/voicemxil/OpenSO/tree/main/TSOClient/FSO.Server/Admin).
The GitHub Actions workflow here checks out that subtree, builds the static bundle
(Node 20 + npm + bower + gulp), and deploys it to **GitHub Pages** at
[admin.openso.org](https://admin.openso.org).

## Updating

The admin UI is rebuilt automatically when this repo is pushed, and can be rebuilt on
demand from the **Actions → "Build & deploy admin webapp to Pages" → Run workflow** button
(use this after changing the admin source upstream).

## Usage

Open <https://admin.openso.org>, log in with an account that has `is_admin=1`
(API URL defaults to `https://api.openso.org`). Authorization is enforced server-side
(`/admin/oauth/token` rejects non-admins), so this public static bundle carries no secrets.

## DNS

`admin.openso.org` is a Pages custom domain — a `CNAME admin.openso.org → voicemxil.github.io`
record points at it (the workflow writes a `CNAME` file into every deploy).
