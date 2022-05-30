FROM alpine 
RUN apk update && apk upgrade
RUN apk add --update lighttpd
COPY ./conf* /etc/lighttpd/
COPY ./html/* /var/www/html
expose 80
CMD ["lighttpd" , "-D" , "-f", "/etc/lighttpd/lighttpd.conf"]

