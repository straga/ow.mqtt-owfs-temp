
Raspberry PI -  Debian “jessie” -  1-wire (owfs)

sudo apt-get install owfs
sudo apt-get install ow-shell
sudo apt-get install python-ownet

В конфиге  /etc/owfs.conf  изменить на реальный USB адаптер.
Bus 001 Device 004: ID 04fa:2490 Dallas Semiconductor DS1490F 2-in-1 Fob, 1-Wire adapter 

У меня 
USB =   DS1490F

Потом можно зайти на http, проверить что все работает.
В консоли можно посматреть тоже.

owdir -s localhost:4304 /

В cc.exe делаем ветку /1-wire. В security даем everyone права.



sudo apt-get install python-mosquitto git
mkdir /etc/mqtt-owfs-temp/

git clone git://github.com/straga/ow.mqtt-owfs-temp.git /usr/local/mqtt-owfs-temp/

Заменяем существующий python-ownet 
git clone git://github.com/straga/ow.python-ownet.git /usr/share/pyshared/ownet/



cp /usr/local/mqtt-owfs-temp/mqtt-owfs-temp.cfg.example /etc/mqtt-owfs-temp/mqtt-owfs-temp.cfg

Копируем список устройств и меняем насвои.
cp /usr/local/mqtt-owfs-temp/devices.csv.sample /etc/mqtt-owfs-temp/devices.csv


cp /usr/local/mqtt-owfs-temp/mqtt-owfs-temp.init /etc/init.d/mqtt-owfs-temp

update-rc.d mqtt-owfs-temp defaults

cp /usr/local/mqtt-owfs-temp/mqtt-owfs-temp.default /etc/default/mqtt-owfs-temp

## Меняем на свои параметры /etc/default/mqtt-owfs-temp and /etc/mqtt-owfs-temp/mqtt-owfs-temp.cfg 

Запустить
/etc/init.d/mqtt-owfs-temp start

За основу было взято.
https://github.com/kylegordon/mqtt-owfs-temp
http://mosquitto.org/documentation/python/
http://wiki.temperatur.nu/index.php/OWFS_with_i2c_support_on_Raspberry_Pi_%28English_version%29





