#docker build -t lucianobrd/httpd httpd/
#docker run -dit --rm --link java --name httpd -p 80:80 lucianobrd/httpd

FROM httpd:2.4
COPY ./app/ /usr/local/apache2/htdocs/
COPY httpd.conf /usr/local/apache2/conf/httpd.conf
#RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf