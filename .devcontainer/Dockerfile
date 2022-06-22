# [Choice] PHP version (use -bullseye variants on local arm64/Apple Silicon): 8, 8.1, 8.0, 7, 7.4, 7.3, 8-bullseye, 8.1-bullseye, 8.0-bullseye, 7-bullseye, 7.4-bullseye, 7.3-bullseye, 8-buster, 8.1-buster, 8.0-buster, 7-buster, 7.4-buster
ARG VARIANT=8-bullseye
FROM mcr.microsoft.com/vscode/devcontainers/php:0-${VARIANT}

COPY php.ini "$PHP_INI_DIR/conf.d/custom.ini"

# Install intl
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
&& apt-get -y install --no-install-recommends libicu-dev \
&& docker-php-ext-install intl

# ** [Optional] Uncomment this section to install additional packages. **
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

ARG MAJORVERSION=1.38
ARG FULLVERSION=1.38.1

RUN curl -o /var/www/html/mediawiki.tar.gz https://releases.wikimedia.org/mediawiki/${MAJORVERSION}/mediawiki-${FULLVERSION}.tar.gz \
&& tar -xf /var/www/html/mediawiki.tar.gz -C /var/www/html \
&& mv /var/www/html/mediawiki-${FULLVERSION} /var/www/html/w \
&& rm /var/www/html/mediawiki.tar.gz \
&& chown -R vscode:www-data /var/www/html/w

# ** Add any custom extensions here like this **
# RUN curl -o /tmp/extension.tar.gz https://extdist.wmflabs.org/dist/extensions/Gadgets-REL1_38-ce7b6bd.tar.gz \
# && tar -xf /tmp/extension.tar.gz -C /var/www/html/w/extensions \
# && rm /tmp/extension.tar.gz

RUN ln -s /workspace /var/www/html/w/extensions/DevExtension \
&& ln -s /workspace/.devcontainer/LocalSettings.php /var/www/html/w/LocalSettings.php \
&& mkdir /var/www/mwsqlite \
&& chmod 770 /var/www/mwsqlite \
&& chown vscode:www-data /var/www/mwsqlite

COPY database.sqlite /var/www/mwsqlite/database.sqlite
RUN chmod 770 /var/www/mwsqlite/database.sqlite \
&& chown vscode:www-data /var/www/mwsqlite/database.sqlite