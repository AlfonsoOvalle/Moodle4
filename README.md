# Instalación Moodle 4 en una distribución de Ubuntu
![N|Solid](https://moodle.org/theme/image.php/moodleorg/theme_moodleorg/1651762895/moodle_logo_small)


>Actualizamos los repositorios
```sh
sudo apt update
```

>Instalar Apache/MySQL/PHP
```sh
sudo apt install apache2 mysql-client mysql-server php7.4 libapache2-mod-php -y
```

>Instalar complementos
```sh
sudo apt install graphviz aspell ghostscript clamav php7.4-pspell php7.4-curl php7.4-gd php7.4-intl php7.4-mysql php7.4-xml php7.4-xmlrpc php7.4-ldap php7.4-zip php7.4-soap php7.4-mbstring -y
```


>Reiniciar Apache
```sh
sudo service apache2 restart
```


>Descargar Moodle 
```sh  
wget https://download.moodle.org/download.php/direct/stable400/moodle-4.0.tgz
```

>Extraer Moodle a /var/www/html  
```sh  
sudo tar zxvf moodle-4.0.tgz -C /var/www/html/
```

>Crear directorios y asignar permisos 
```sh  
sudo mkdir /var/moodledata
sudo chown -R www-data /var/moodledata
sudo chmod -R 777 /var/moodledata
sudo chmod -R 0755 /var/www/html/moodle
sudo chmod -R 777 /var/www
```

>Crear Base de datos Moodle  
```sh  
sudo mysql --user="root" --password="$password" --execute="CREATE DATABASE IF NOT EXISTS moodle DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;"
```

>Crear usuarios 
```sh  
sudo mysql --user="root" --password="$password" --execute="create user 'moodledude'@'localhost' IDENTIFIED BY 'passwordformoodledude';"
```

>Asignar permisos al usuario moodledude 
```sh  
sudo mysql --user="root" --password="$password" --execute="GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,CREATE TEMPORARY TABLES,DROP,INDEX,ALTER ON moodle.* TO 'moodledude'@'localhost';"
```

>Abriendo el servidor de moodle
```sh  
xdg-open http://localhost/moodle
```

# Script Completo 

>script.sh
```sh  

#!/bin/bash
password=

echo -e "\e[32m ####################### Actualizando repositorios ####################### \e[0m"
sudo apt update


echo -e "\e[32m ####################### Instalar Apache/MySQL/PHP ####################### \e[0m"
sudo apt install apache2 mysql-client mysql-server php7.4 libapache2-mod-php -y

echo -e "\e[32m ####################### Instalar complementos ####################### \e[0m"
sudo apt install graphviz aspell ghostscript clamav php7.4-pspell php7.4-curl php7.4-gd php7.4-intl php7.4-mysql php7.4-xml php7.4-xmlrpc php7.4-ldap php7.4-zip php7.4-soap php7.4-mbstring -y


echo -e "\e[32m ####################### Reiniciar Apache ####################### \e[0m"
sudo service apache2 restart


echo -e "\e[32m ####################### Descargar Moodle ####################### \e[0m"

  if [[ -f moodle-4.0.tgz ]]
  then
    #Existe el archivo
    sudo rm -r moodle-4.0.tgz
  fi
  
  if [[ -d /var/www/html/moodle ]]
  then
    #Existe el directorio
    sudo rm -r /var/www/html/moodle
  fi  
  
wget https://download.moodle.org/download.php/direct/stable400/moodle-4.0.tgz

echo -e "\e[32m ####################### Extraer Moodle a /var/www/html ####################### \e[0m"
sudo tar zxvf moodle-4.0.tgz -C /var/www/html/


echo -e "\e[32m ####################### Crear directorios y asignar permisos ####################### \e[0m"
  if [[ -d /var/moodledata ]]
  then
    #Existe el directorio
    echo -e "\e[32m ####################### removiendo el directorio /var/moodledata ####################### \e[0m"
    sudo rm -r /var/moodledata
  fi
sudo mkdir /var/moodledata
sudo chown -R www-data /var/moodledata
sudo chmod -R 777 /var/moodledata
sudo chmod -R 0755 /var/www/html/moodle
sudo chmod -R 777 /var/www


echo -e "\e[32m ####################### Crear Base de datos Moodle ####################### \e[0m"
sudo mysql --user="root" --password="$password" --execute="CREATE DATABASE IF NOT EXISTS moodle DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;"

echo -e "\e[32m ####################### Crear usuarios ####################### \e[0m"
sudo mysql --user="root" --password="$password" --execute="create user 'moodledude'@'localhost' IDENTIFIED BY 'passwordformoodledude';"

echo -e "\e[32m ####################### Asignar permisos al usuario moodledude ####################### \e[0m"
sudo mysql --user="root" --password="$password" --execute="GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,CREATE TEMPORARY TABLES,DROP,INDEX,ALTER ON moodle.* TO 'moodledude'@'localhost';"

echo -e "\e[32m ####################### Abriendo el servidor de moodle ####################### \e[0m"
xdg-open http://localhost/moodle


```

# Uso

>Ejecutar Script
```sh  
./script.sh
```

# Moodle 4
![N|Solid](https://www.evirtualplus.com/wp-content/uploads/2016/08/moodle-instalacion-1.jpg.webp)



