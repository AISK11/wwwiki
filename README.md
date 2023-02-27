# wwwiki

*- personal web knowledge base project.*

## Installation

### Debian Linux

1. Install dependency packages:

```console
root@debian# apt install -y git rsync nginx php-fpm php-xml
```

2. Download  and install DokuWiki:

    - Navigate to [DokuWiki Download](https://download.dokuwiki.org/) page.
    - Toggle all languages and click Download.
    - Extract DokuWiki to the webserver:

```console
root@debian# tar xvzf <dokuwiki-XXX.tgz> -C /var/www/
```

3. Copy and install this repository (**trailing slashes are important!**):

```console
root@debian# git clone https://github.com/aisk11/wwwiki
root@debian# rsync -av ./wwwiki/backend/nginx/nginx.conf /etc/nginx/nginx.conf
root@debian# rsync -av --delete ./wwwiki/frontend/dokuwiki/conf/ /var/www/dokuwiki/conf/
root@debian# rsync -av --delete ./wwwiki/frontend/dokuwiki/lib/ /var/www/dokuwiki/lib/
root@debian# rsync -av --delete ./wwwiki/frontend/dokuwiki/data/pages/ /var/www/dokuwiki/data/pages/
root@debian# rsync -av --delete ./wwwiki/frontend/dokuwiki/data/attic/ /var/www/dokuwiki/data/attic/
root@debian# rsync -av --delete ./wwwiki/frontend/dokuwiki/data/meta/ /var/www/dokuwiki/data/meta/
root@debian# rsync -av --delete ./wwwiki/frontend/dokuwiki/data/media/ /var/www/dokuwiki/data/media/
root@debian# rsync -av --delete ./wwwiki/frontend/dokuwiki/data/media_attic/ /var/www/dokuwiki/data/media_attic/
root@debian# rsync -av --delete ./wwwiki/frontend/dokuwiki/data/media_meta/ /var/www/dokuwiki/data/media_meta/
```

4. Correct permissions:

```console
root@debian# chown -R www-data:www-data /var/www/dokuwiki/
```

5. Enable and start webserver services:

```console
root@debian# PHP_VERSION=$(php -v | cut -d ' ' -f 2 | grep -Eo '[0-9]*\.[0-9]*' | head -n 1)
root@debian# systemctl enable "php${PHP_VERSION}-fpm.service"
root@debian# systemctl start "php${PHP_VERSION}-fpm.service"
root@debian# systemctl enable "nginx.service"
root@debian# systemctl start "nginx.service"
```

6. Navigate to [http://localhost](http://localhost) and login as admin:admin.
