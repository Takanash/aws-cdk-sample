FROM nginx:1.15.8

RUN rm -f /etc/nginx/conf.d/*

ADD nginx.conf /etc/nginx/conf.d/myapp.conf
CMD /usr/sbin/nginx -g 'daemon off;' -c /etc/nginx/nginx.conf
