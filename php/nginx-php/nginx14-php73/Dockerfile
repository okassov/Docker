FROM ubuntu:18.04
MAINTAINER Okassov Marat - DevOps Technodom <dmao@technodom.kz>

ENV NGINX_VERSION 1.14.0-0~bionic
ENV TZ=Asia/Almaty

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update \
 && DEBIAN_FRONTEND=noninteractive \ 
 && export LC_ALL=en_US.UTF-8 \
 && export LANG=en_US.UTF-8 \     
 && apt-get update \
 && apt-get install -y \
        language-pack-en-base \
        software-properties-common \
 && add-apt-repository ppa:ondrej/php -y \
 && apt-get update \
 && apt-get install \
        --no-install-recommends \
        --no-install-suggests -y \            
        ca-certificates \  
        php7.3 \  
        php7.3-mbstring \
        php7.3-xml \        
        php7.3-fpm \           
        php7.3-gd \          
        php7.3-curl \            
        php7.3-imagick \            
        php7.3-pgsql \         
        php7.3-mysql \           
        php7.3-opcache \            
        php7.3-zip \       
        php7.3-soap \            
        php7.3-xsl \          
        php7.3-intl \            
        php-memcached \            
        php-memcache \          
        curl \   
        openssl \             
        ca-certificates \
        wget \
        libwww-perl \
        libcrypt-ssleay-perl \
        rsyslog \
        run-one \           
        sudo \        
        ssmtp \            
        python-pip \
        python-setuptools \            
        supervisor \
 && echo "deb http://nginx.org/packages/mainline/ubuntu/ bionic nginx" > /etc/apt/sources.list.d/nginx.list \
 && wget -O /tmp/nginx_signing.key http://nginx.org/keys/nginx_signing.key \
 && apt-key add /tmp/nginx_signing.key \
 && apt-get update \
 && apt-get install \
        --no-install-recommends \
        --no-install-suggests -y nginx \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN pip install supervisor-stdout

# Forward request and error logs to STDOUT and STDERR
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
 && ln -sf /dev/stderr /var/log/nginx/error.log

# NGINX configuration copy
COPY conf/nginx /etc/nginx

# PHP configuration copy
COPY conf/php/7.3 /etc/php/7.3/
RUN sed -i -e "s/;\?daemonize\s*=\s*yes/daemonize = no/" /etc/php/7.3/fpm/php-fpm.conf
RUN mkdir -p /run/php /var/log/app_engine && chown www-data.www-data /run/php

# SUPERVISOR configuration copy
COPY conf/supervisor/supervisord.conf /etc/supervisor/supervisord.conf

CMD /usr/bin/supervisord -c /etc/supervisor/supervisord.conf

