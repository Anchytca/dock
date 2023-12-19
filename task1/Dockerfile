FROM ubuntu:20.04

WORKDIR /home/linuxlite/dock/task1

RUN apt update && \
	apt install -y -q nginx && \
	apt-get clean && \
	rm -rf /var/www && \
	mkdir -p /var/www && \
	mkdir -p /var/www/my_project && \
	mkdir -p /var/www/my_project/img && \
	chmod -R u+rwX,go+rX,go-w /var/www/my_project && \
	useradd user1 && \
	groupadd group1 && \
	usermod -aG group1 user1 && \
	chown -R user1:group1 /var/www/my_project && \
	chgrp -R group1 /var/www/my_project

COPY index.html /var/www/my_project/index.html
COPY volk.jpg /var/www/my_project/img/volk.jpg
COPY default /etc/nginx/sites-available/default

RUN sed -i 's# /var/www/html# /var/www/my_project#' /etc/nginx/sites-available/default && \
	sed -i 's# user www-data;# user user1;#' /etc/nginx/nginx.conf

EXPOSE 8080/tcp

CMD ["/usr/sbin/nginx", "-g", "daemon off;"]