FROM php:7.4.28-apache

RUN apt-get update
RUN apt-get upgrade -y

RUN apt-get install --fix-missing -y libpq-dev
RUN apt-get install --no-install-recommends -y libpq-dev
RUN apt-get install -y libxml2-dev libbz2-dev zlib1g-dev
RUN apt-get -y install libsqlite3-dev libsqlite3-0 mariadb-client curl exif ftp
RUN docker-php-ext-install intl
RUN apt-get -y install --fix-missing zip unzip vim

# RUN printf "#!/bin/bash\nmv /codeigniter4 /var/www/html\n/usr/sbin/apache2ctl -D FOREGROUND" > /startScript.sh
# RUN chmod +x /startScript.sh

# Composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer
RUN composer self-update

# RUN cd /var/www/html
# RUN cd /
# RUN composer create-project codeigniter4/appstarter codeigniter4
# RUN chmod -R 0777 /var/www/html/codeigniter4/writable

RUN apt-get clean \
    && rm -r /var/lib/apt/lists/*

RUN printf "#!/bin/bash\ncd /\ncomposer create-project codeigniter4/appstarter codeigniter4\nmv /codeigniter4 /var/www/html\nchmod -R 0777 /var/www/html/codeigniter4/writable\n/usr/sbin/apache2ctl -D FOREGROUND" > /startScript.sh

RUN chmod +x /startScript.sh    

VOLUME ['/var/www/html']

CMD ["bash", "/startScript.sh"]