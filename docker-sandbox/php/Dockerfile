FROM centos:7

MAINTAINER Federico Garcia <fgarcia@urbano.com.ar>

RUN echo "Starting to setup Docker"

RUN echo "Installing EPEL Repo"
# Install EPEL Repo
RUN yum -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
RUN yum -y install http://rpms.remirepo.net/enterprise/remi-release-7.rpm

RUN echo "Installing PHP5.6 and modules"
# Install PHP
RUN yum install yum-utils
RUN yum-config-manager --enable remi-php56
RUN yum -y install php php-bcmath php-cli php-common php-gd php-intl php-ldap php-mbstring \
    php-mysql php-mssql php-pear php-soap php-xml php-xmlrpc php-pecl php-pdo pmbstringhp-zts php-devel php-mcrypt php-fileinfo

RUN echo "Copying PDO Informix and SKD"
RUN yum install -y wget git glibc gcc make
WORKDIR /opt
COPY pdo_informix/clientsdk.4.10.FC7DE.LINUX.tar.gz /opt/clientsdk.4.10.FC7DE.LINUX.tar.gz
RUN wget https://pecl.php.net/get/PDO_INFORMIX-1.3.3.tgz
COPY pdo_informix/pdo_informix.ini /etc/php.d/pdo_informix.ini

RUN echo "Extracting PDO Informix and sdk"
RUN tar -xzvf clientsdk.4.10.FC7DE.LINUX.tar.gz
RUN tar -xzvf PDO_INFORMIX-1.3.3.tgz

RUN echo "Silent installer Informix SDK"
WORKDIR /opt/clientsdk.4.10.FC7DE.LINUX
RUN chmod +x installclientsdk
RUN ./installclientsdk -i silent -DLICENSE_ACCEPTED=TRUE -DPRQCHECK=FALSE

RUN echo "Installer PDO"
WORKDIR /opt/PDO_INFORMIX-1.3.3
RUN phpize
RUN ./configure --with-pdo-informix=/opt/IBM/informix
WORKDIR /opt/PDO_INFORMIX-1.3.3
RUN make
RUN make install

