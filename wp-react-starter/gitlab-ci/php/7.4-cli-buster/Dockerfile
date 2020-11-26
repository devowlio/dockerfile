# This image also includes the brand new Composer v2 and Cypress v5 dependencies !

FROM php:7.4-cli-buster

# Apt and common dependencies
RUN apt-get update && apt-get install -y \
    # Commons
    sudo \
    autogen \
    wget \
    zip \
    unzip \
    tar \
    git \
    subversion \
    build-essential \
    apt-utils \
    software-properties-common \
    nasm \
    libjpeg-dev \
    libpng-dev \
    libpng16-16 \
    # Allow simple FTP uploads
    lftp \
    wput \
    # Pyhton is needed for Docker-Compose
    python \
    python-pip \
    python-dev \
    # Cypress.io dependencies
    xvfb \
    libgtk2.0-0 \
    libgtk-3-0 \
    libgbm-dev \
    libnotify-dev \
    libgconf-2-4 \
    libnss3 \
    libxss1 \
    libasound2 \
    libxtst6 \
    xauth \
    # libssl-dev is needed for Phar (https://raspberrypi.stackexchange.com/a/36379)
    libssl-dev && \
    # PHP dependencies (https://git.io/JvAFa)
    docker-php-ext-install -j4 phar json mbstring tokenizer && \
    # xdebug (can be activated with `docker-php-ext-enable xdebug`, not by default because it slows down PHP)
    pecl install xdebug && \
    # Composer
    curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    chmod +x /usr/local/bin/composer && \
    composer self-update && \
    # Node
    curl -sL https://deb.nodesource.com/setup_12.x -o nodesource_setup.sh && \
    bash nodesource_setup.sh && \
    apt-get install -y nodejs && \
    # Yarn
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install -y yarn && \
    # Docker and Docker-Compose
    curl -sSL https://get.docker.com/ | sh && \
    curl -L "https://github.com/docker/compose/releases/download/$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep -oP '"tag_name": "\K(.*)(?=")')/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && \
    chmod +x /usr/local/bin/docker-compose && \
    # WP CLI
    curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && \
    php wp-cli.phar --info && \
    chmod +x wp-cli.phar && \
    mv wp-cli.phar /usr/local/bin/wp && \
    # PHP Scoper
    curl -O -L https://github.com/humbug/php-scoper/releases/download/0.13.1/php-scoper.phar && \
    chmod +x php-scoper.phar && \
    mv php-scoper.phar /usr/local/bin/php-scoper && \
    # ets: Command output timestamper
    wget -c https://github.com/zmwangx/ets/releases/download/$(curl -s https://api.github.com/repos/zmwangx/ets/releases/latest | grep -oP '"tag_name": "\K(.*)(?=")')/ets_$(curl -s https://api.github.com/repos/zmwangx/ets/releases/latest | grep -oP '"tag_name": "v\K(.*)(?=")')_linux_$(dpkg --print-architecture).tar.gz -O - | tar -xz -C /usr/local/bin

RUN npm install -g \
    # Global installations of npm packages
    wait-on
