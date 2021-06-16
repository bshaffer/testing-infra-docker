FROM gcr.io/gcp-runtimes/ubuntu_18_0_4

ENV PHPBREW_ROOT /root/.phpbrew
ENV PHPBREW_HOME /root/.phpbrew
ENV PHPBREW_SET_PROMPT 1
# ENV PHP74_VERSION 7.4.28
# ENV PHP80_VERSION 7.3.28

# ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update \
  && apt-get -qqy install git \
  && apt-get -qqy install wget \
  && apt-get -qqy install curl \
  && apt-get -qqy install ant ant-contrib sqlite3 \
  && apt-get -qqy install \
      autoconf \
      build-essential \
      libbz2-dev \
      libreadline-dev \
      libsqlite3-dev \
      libssl-dev \
      libxml2-dev \
      libxslt1-dev \
      libonig-dev \
      php7.2-cli \
      php7.2-bz2 \
      pkg-config \
      libcurl4-gnutls-dev \
      libzip-dev zip \
      libmagickwand-dev \
      php-imagick \
      jq \
  && apt-get clean -y \
  && apt-get autoclean -y \
  && apt-get autoremove -y \
  && rm -rf /var/lib/{apt,dpkg,cache,log}/ \
  && rm -rf /var/lib/apt/lists/*

RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# Install and initialize PHPBrew
RUN mkdir -p /usr/bin/ \
    && wget -q -O /usr/bin/phpbrew https://github.com/phpbrew/phpbrew/raw/master/phpbrew \
    && chmod +x /usr/bin/phpbrew \
    && phpbrew init \
    && echo 'source $HOME/.phpbrew/bashrc' >> /root/.bashrc

ENV PHP73_VERSION 7.3.28
ENV PHP74_VERSION 7.4.20
ENV PHP80_VERSION 8.0.7

RUN phpbrew install "7.3" \
    +default +bcmath +bz2 +calendar +cli +ctype +dom +fileinfo +filter +json \
    +mbregex +mbstring +mhash +pcntl +pcre +pdo +phar +posix +readline +sockets \
    +tokenizer +xml +curl +zip +openssl=yes +opcache +fpm +sqlite +mysql \
    +default +intl +gettext

RUN phpbrew install "7.4" \
    +default +bcmath +bz2 +calendar +cli +ctype +dom +fileinfo +filter +json \
    +mbregex +mbstring +mhash +pcntl +pcre +pdo +phar +posix +readline +sockets \
    +tokenizer +xml +curl +zip +openssl=yes +opcache +fpm +sqlite +mysql \
    +default +intl +gettext

RUN phpbrew install "8.0" \
    +default +bcmath +bz2 +calendar +cli +ctype +dom +fileinfo +filter +json \
    +mbregex +mbstring +mhash +pcntl +pcre +pdo +phar +posix +readline +sockets \
    +tokenizer +xml +curl +zip +openssl=yes +opcache +fpm +sqlite +mysql \
    +default +intl +gettext

# RUN source ~/.phpbrew/bashrc \
#     && phpbrew each \
#         phpbrew ext install grpc \
#         && phpbrew ext install imagick \
#         && phpbrew ext install memcache \
#         && phpbrew ext enable opcache

# RUN apt-get update && \
#     apt-get -y install \
#             autoconf \
#             build-essential \
#             git-core \
#             jq \
#             memcached \
#             php-imagick \
#             php-memcached \
#             python-ipaddr \
#             wget \
#             zip \
#             zlib1g-dev \
#             pkg-config \
#             sqlite3 \
#             libsqlite3-dev \
#             libonig-dev \
#             php-pear

# # # Install composer
# RUN wget -q -O /usr/bin/composer https://getcomposer.org/composer.phar && chmod +x /usr/bin/composer

# # # Install Google Cloud SDK
# RUN curl https://dl.google.com/dl/cloudsdk/release/google-cloud-sdk.tar.gz \
#         -o ${HOME}/google-cloud-sdk.tar.gz \
#     && tar xzf ${HOME}/google-cloud-sdk.tar.gz -C $HOME \
#     && ${HOME}/google-cloud-sdk/install.sh \
#         --usage-reporting false \
#         --path-update false \
#         --command-completion false \
#     && source ${HOME}/google-cloud-sdk/path.bash.inc

# # Configure Google Cloud SDK
# RUN gcloud config set app/promote_by_default false && \
#     gcloud config set disable_prompts true && \
#     gcloud -q components install app-engine-python && \
#     gcloud -q components update

# # # Install Cloud SQL proxy
# RUN wget https://dl.google.com/cloudsql/cloud_sql_proxy.linux.amd64 -O cloud_sql_proxy \
#     && chmod +x cloud_sql_proxy \
#     && mv cloud_sql_proxy /usr/local/bin

# # # Build php-cs-fixer
# RUN composer global require friendsofphp/php-cs-fixer

# # # Make composer and gcloud bins available via the PATH variable
# ENV PATH="$PATH:/root/.config/composer/vendor/bin:/root/google-cloud-sdk/bin"
