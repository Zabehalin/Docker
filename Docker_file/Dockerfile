FROM centos:7
MAINTAINER zabehalin
RUN yum -y install httpd && yum -y install bash && yum -y install php-gd && yum -y install wget && yum -y install nano && yum -y install firewalld
RUN yum -y install epel-release yum-utils
RUN yum -y install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
RUN yum-config-manager --enable remi-php73
RUN yum -y install php && yum -y install  php-common && yum -y install  php-opcache && yum -y install php-mcrypt && yum -y install php-cli && yum -y install php-gd && yum -y install php-curl && yum -y install php-mysqlnd     
RUN yum clean all
RUN wget http://wordpress.org/latest.tar.gz
RUN tar -xzvf latest.tar.gz
RUN cp -avr wordpress/* /var/www/html/
RUN mkdir /var/www/html/wp-content/uploads
RUN chown -R apache:apache /var/www/html/
RUN chmod -R 755 /var/www/html/
RUN mv /var/www/html/wp-config-sample.php /var/www/html/wp-config.php
RUN grep -rl username_here /var/www/html/wp-config.php* | xargs perl -p -i -e 's/username_here/wordpress3/g'
RUN grep -rl database_name_here /var/www/html/wp-config.php* | xargs perl -p -i -e 's/database_name_here/root/g'
RUN grep -rl password_here /var/www/html/wp-config.php* | xargs perl -p -i -e 's/password_here/my-secret-pass/g'
RUN grep -rl localhost /var/www/html/wp-config.php* | xargs perl -p -i -e 's/localhost/13.53.146.168/g'

#RUN firewall-cmd --permanent --zone=public --add-service=http
#RUN firewall-cmd --permanent --zone=public --add-service=https
#RUN firewall-cmd --reload
CMD [ "httpd" ]
CMD [ "firewalld" ]
CMD ["/usr/sbin/init"]
