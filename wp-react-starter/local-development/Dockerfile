FROM php:7.3-cli-stretch

RUN apt-get update && apt-get install -y \
    # Commons
    sudo \
    nano \  
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
    # Pyhton is needed for Docker-Compose
    python \
    python-pip \
    python-dev \
    # Cypress.io dependencies
    xvfb \
    libgtk2.0-0 \
    libgtk-3-0 \
    libnotify-dev \
    libgconf-2-4 \
    libnss3 \
    libxss1 \
    libasound2 \
    libxtst6 \
    xauth \
    # libssl-dev is needed for Phar (https://raspberrypi.stackexchange.com/a/36379)
    libssl-dev

# PHP dependencies (https://git.io/JvAFa)
RUN docker-php-ext-install -j4 phar json mbstring tokenizer 

# xdebug (can be activated with `docker-php-ext-enable xdebug`, not by default because it slows down PHP)
RUN  pecl install xdebug

# Composer
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    chmod +x /usr/local/bin/composer

# Prestissimo for Composer
RUN composer global require hirak/prestissimo=0.3.10

# Node 
RUN curl -sL https://deb.nodesource.com/setup_12.x -o nodesource_setup.sh && \
    bash nodesource_setup.sh && \
    apt-get install -y nodejs

# Yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install -y yarn

# Docker and Docker-Compose (via Python, PiP)
RUN curl -sSL https://get.docker.com/ | sh && \
    pip install docker-compose

# WP CLI
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && \
    php wp-cli.phar --info && \
    chmod +x wp-cli.phar && \
    mv wp-cli.phar /usr/local/bin/wp

# PHP Scoper
RUN curl -O -L https://github.com/humbug/php-scoper/releases/download/0.13.1/php-scoper.phar && \
    chmod +x php-scoper.phar && \
    mv php-scoper.phar /usr/local/bin/php-scoper

# Global installations of npm packages
RUN npm install -g \
    wait-on \
    create-wp-react-app

# Create non-root user
RUN adduser --disabled-password --gecos "" developer && usermod -aG docker developer
RUN echo "developer ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
USER developer
