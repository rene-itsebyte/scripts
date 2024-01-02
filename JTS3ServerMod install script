#!/bin/bash

if [ "$UID" -ne 0 ]; then
    echo "You must be root!."
    exit 1
fi

echo "You are root script is running."

DIR="/root/"
DATEI="/etc/apt/sources.list.d/mariadb.sources"
VER="8.3"
LINK="https://www.stefan1200.de/dlrequest.php?file=privatejts3servermodhostingedition&type=.zip"
BOT="JTS3ServerMod_HostingEdition_6.5.8.zip"
DATA="JTS3ServerMod_HostingEdition"
INHALT="# MariaDB 11.2 repository list - created 2023-12-29 18:01 UTC
# https://mariadb.org/download/
X-Repolib-Name: MariaDB
Types: deb
# deb.mariadb.org is a dynamic mirror if your preferred mirror goes offline. See https://mariadb.org/mirrorbits/ for details.
# URIs: https://deb.mariadb.org/11.2/debian
URIs: https://mirror1.hs-esslingen.de/pub/Mirrors/mariadb/repo/11.2/debian
Suites: bookworm
Components: main
Signed-By: /etc/apt/keyrings/mariadb-keyring.pgp"

apt update
apt upgrade
apt dist-upgrade

echo "System is patched."

echo "Starting with Install"

sleep 4

cd $dir

apt -y install software-properties-common curl ca-certificates gnupg2 sudo lsb-release unzip default-jre apt-transport-https

mkdir -p /etc/apt/keyrings

curl -o /etc/apt/keyrings/mariadb-keyring.pgp 'https://mariadb.org/mariadb_release_signing_key.pgp'

echo "$INHALT" > "$DATEI"

apt-get update -y 

echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | tee /etc/apt/sources.list.d/sury-php.list
curl -fsSL https://packages.sury.org/php/apt.gpg | gpg --dearmor -o /etc/apt/trusted.gpg.d/sury-keyring.gpg

apt update -y

apt install -y php$VER php$VER-{common,cli,gd,mysql,mbstring,bcmath,xml,fpm,curl,zip}

apt install -y php$VER-ssh2

apt install -y mariadb-server

mysql_secure_installation

mysql -u root



wget $LINK
unzip $BOT
cd $DATA
cp /webinterface /var/www/webinterface
chmod -R 777 /var/www/webinterface
cd $DIR
cp $DATA /opt/controlbot
chmod -R 777 /opt/controlbot

