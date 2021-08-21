FROM centos:7

RUN yum install epel-release -y && yum update -y && yum install nginx -y && systemctl enable nginx && systemctl start nginx && yum install redis -y && systemctl enable redis && systemctl start redis && yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm -y && yum install yum-utils -y && yum-config-manager --enable remi-php73 && yum install php php-bz2 php-ctype php-mcrypt php-cli php-gd php-mbstring php-common php-curl php-xml php-mysql php-ldap php-zip php-fileinfo php-pear php-devel -y && pecl install igbinary igbinary-devel redis

COPY ./index.html /var/www/html/index.html

RUN chown -Rf www-data:www-data /var/www/html

WORKDIR /var/www/html

RUN chmod -Rf 775 /var/www/html

EXPOSE 80 443 6379

RUN yum install mod_ssl -y

ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]

CMD ["-D", "FOREGROUND"]
