FROM wordpress:5.8.1-apache

# Apt and common dependencies
RUN apt-get update && apt-get install -y \
    # The database needs to be ready, so netcat it, and also the wp binary must be downloaded and executable
    netcat \
    # We need the mariadb-client so mysqldump can be used by WP-CLI
    mariadb-client && \
    # Install imagemagick (https://stackoverflow.com/a/49427273/5506547)
    apt-get -y install libmagickwand-dev --no-install-recommends && \
    pecl install imagick && \
    docker-php-ext-enable imagick && \
    # WP CLI
    curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && \
    php wp-cli.phar --info && \
    chmod +x wp-cli.phar && \
    mv wp-cli.phar /usr/local/bin/wp && \
    . ~/.bashrc
