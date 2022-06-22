# (Unofficial) MediaWiki Codespaces template for developing extensions
Codespaces template for developing extensions for MediaWiki

You can start the HTTP server with `sudo apache2ctl start`.

## Setup
- Complete the usual setup at `/w/mw-config`
- - Database: SQLite; Directory: `/var/www/mwsqlite`; Name: `database`
- Paste the LocalSettings into `./.devcontainer/LocalSettings.php`, so it persists after Codespace rebuilds.
- Copy the database from `/var/www/mwsqlite/database.sqlite` to `./.devcontainer/database.sqlite`, for the same reason as above.
- - `cp /var/www/mwsqlite/database.sqlite /workspace/.devcontainer/database.sqlite`
- - You can repeat the above step anytime you make changes to the database that you want to persist after Codespace rebuilds.

## Configuration
Check `devcontainer.json` for configurable args