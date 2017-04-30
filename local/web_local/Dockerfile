FROM php:7.1.3-apache
MAINTAINER kaotil

RUN apt-get update && apt-get install -y \
  vim \
  git \
  locales

RUN locale-gen ja_JP.UTF-8  
ENV LANG ja_JP.UTF-8  
ENV LANGUAGE ja_JP:en  
ENV LC_ALL ja_JP.UTF-8
RUN localedef -f UTF-8 -i ja_JP ja_JP.UTF-8

RUN ln -fs /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

COPY kaotil-default.conf /etc/apache2/sites-available/kaotil-default.conf
RUN sed -i 's/ServerTokens OS/ServerTokens Prod/' /etc/apache2/conf-available/security.conf
RUN sed -i 's/ServerSignature On/ServerSignature Off/' /etc/apache2/conf-available/security.conf
RUN a2ensite kaotil-default.conf
RUN a2dissite 000-default.conf
RUN a2enmod rewrite

#RUN mkdir -p /opt/web/
#ADD ../src /opt/web/
#WORKDIR /opt/web/
#RUN git clone https://github.com/kaotil/kaotil.com.git

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
