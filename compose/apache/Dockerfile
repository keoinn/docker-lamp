FROM httpd:2.4-alpine
ARG HTTPD_ADMIN
ENV APACHE_LOG_DIR /usr/local/apache2/logs
RUN touch /tmp/new_apache.conf && \
    cat /usr/local/apache2/conf/original/httpd.conf > /tmp/new_apache.conf && \
    echo "Include /usr/local/apache2/conf.d/*.conf" >> /tmp/new_apache.conf && \
    mv /tmp/new_apache.conf /usr/local/apache2/conf/httpd.conf && \
    # Enable module
    sed -i 's/#LoadModule rewrite_module modules\/mod_rewrite.so/LoadModule rewrite_module modules\/mod_rewrite.so/g' /usr/local/apache2/conf/httpd.conf && \
    sed -i 's/#LoadModule proxy_fcgi_module modules\/mod_proxy_fcgi.so/LoadModule proxy_fcgi_module modules\/mod_proxy_fcgi.so/g' /usr/local/apache2/conf/httpd.conf && \
    sed -i 's/#LoadModule proxy_module modules\/mod_proxy.so/LoadModule proxy_module modules\/mod_proxy.so/g' /usr/local/apache2/conf/httpd.conf && \
    sed -i 's/#LoadModule deflate_module modules\/mod_deflate.so/LoadModule deflate_module modules\/mod_deflate.so/g' /usr/local/apache2/conf/httpd.conf && \
    #Apache2 Server Settings
    sed -i 's/DirectoryIndex index.html/DirectoryIndex index.php index.html/g' /usr/local/apache2/conf/httpd.conf && \
    sed -i "s/ServerAdmin you@example.com/ServerAdmin ${HTTPD_ADMIN}/g" /usr/local/apache2/conf/httpd.conf && \
    sed -i "s/#ServerName www.example.com:80/ServerName localhost/g" /usr/local/apache2/conf/httpd.conf && \
    sed -i 's#/usr/local/apache2/htdocs#/var/www/html#g' /usr/local/apache2/conf/httpd.conf