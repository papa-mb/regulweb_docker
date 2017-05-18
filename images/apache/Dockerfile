FROM sigsciserverimg/centos_6-apache_2.2.15_native

ENV ANT_HOME /home/www-data/apache-ant/apache-ant-1.9.6
ENV PHP_TOOLS /home/www-data/phptools
ENV JAVA_HOME /opt/jdk1.8.0_45

RUN groupadd www-data -g 1000
RUN useradd www-data -u 1000 -g 1000 -p 'saopPGHdx.TEk'

RUN echo ANT_HOME=$ANT_HOME >> /home/www-data/.bashrc &&\
    echo PHP_TOOLS=$PHP_TOOLS >> /home/www-data/.bashrc &&\
    echo JAVA_HOME=$JAVA_HOME >> /home/www-data/.bashrc
RUN echo PATH=$JAVA_HOME/bin:$PHP_TOOLS/bin:$ANT_HOME/bin:$PATH >> /home/www-data/.bashrc
RUN sed -i 's|^;date.timezone =.*$|date.timezone = Europe/Paris|' /etc/php.ini
RUN sed -i 's|session.save_path.*$|session.save_path = "/home/www-data/sessions"|' /etc/php.ini
RUN sed -i 's|memory_limit =|memory_limit = -1|' /etc/php.ini
RUN mkdir /home/www-data/sessions && chown www-data:www-data /home/www-data/sessions && chmod 700 /home/www-data/sessions

RUN yum install -y php-mysql php-devel php-gd php-pecl-memcache php-pspell php-snmp php-xmlrpc php-xml php-ldap\
    mysql git

COPY apache-foreground /usr/local/bin/
RUN mkdir /etc/httpd/vh
COPY vh/* /etc/httpd/vh/
RUN mv /etc/httpd/conf/httpd.conf /etc/httpd/conf/httpd.conf.bck
COPY httpd.conf /etc/httpd/conf/httpd.conf

EXPOSE 80 25

CMD ["apache-foreground"]
