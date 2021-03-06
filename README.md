# Блог для компании "Трия" (тестовое задание)
Инструкция по развёртыванию установленного сайта
# Установка и настройка сервера
### Установка сервера WAMP64. 
Дистрибутив сервера расположен по ссылке https://disk.yandex.ru/d/VXDAplm_zdybpg. Если устновщик обнаружит, что в системе отсутствует пакет Microsoft Visual C++ Redistributable, то подтвердите установку покета. После этого снова запустите установщик WAMP64.
Директорию установки оставьте по умолчанию C:/wamp64. На следующих шагах выберите версии PHP 7.3.12 и MySQL 8.0.18.
### Настройка модулей
После установки запустите WAMP64, подождите 10-15 секунд до момента появления значка сервера в трее. Правой кнопкой мыши вызовите меню и выполните следующие действия в пункте меню "Tools":
1) в секции Default DBMS переключите движок базы данных на MySQL (Invert deafult DBMS...);
2) в пункте "Change CLI PHP version" выберите "PHP 7.3.12";
3) запустите любой браузер и в адресной строке напишите http:/localhost.
Должна отобразиться информационная страница сервера.
### Установка Composer
Дистрибутив с официального сайта https://getcomposer.org/. 
### Настройка виртуального сервера
Алгоритм:
1) В папке c:\wamp64 создать папку с именем blog.local
2) Открыть папку C:\wamp64\bin\apache\apache2.4.41\conf\extra\;
3) Открыть в текстовом редакторе от имени администратора файл httpd-vhosts.conf;
4) Добавить в файл следующие строки:  
<VirtualHost *:80>  
ServerName blog.local  
DocumentRoot "${INSTALL_DIR}/www/blog.local/laravel/public"  
<Directory "${INSTALL_DIR}/www/blog.local/laravel/public">  
AllowOverride All  
Require all granted  
<\/Directory>  
<\/VirtualHost>  
5) в файл hosts системы внести строку:  
    127.0.0.1 blog.local 
# Развёртывание сайта
### Копирование файлов
Распакуйте папку blog.local из архива в папку C:\wamp64\www\.  
Всё, что нужно для работы сайта, будет расположено по адресу:  
C:\wamp64\www\blog.local\laravel\.
### Создание базы данных
С информационной страницы сервера перейдите по ссылке phpmyadmin и задайте параметры входа:
1) имя пользователя root;
2) пароль PASSWORD;  
Примечание: одна из страниц сайта использует связь с базой данных собственными средствами mysql, средства laravel позволяют не писать данные для входа в коде страницы.
3) создайте базу данных с именем 'tolstov_bd' и кодировкой 'utf8_unicode_ci';
4) запустите терминал сервера;
5) запустите миграцию командой:  
    php artisan migrate.  
6) убедитесь, что в базе данных созданы таблицы: posts, users, subscriptions. 
7) запустите заполнение таблиц фиктивными данными в следующем порядке:  
    php artisan db:seed --class=UserSeeder  
    php artisan db:seed --class=PostSeeder  
    php artisan db:seed --class=SubsSeeder  
В результате в БД появятся 10 пользователей сайта, 20 постов; 20 случайно распределённых подписок пользователей друг на друга.
# Вход на сайт
Для входа на сайт требуется e-mail и пароль. Для сгенерированных пользователей:  
e-mail: author_Z@example.ru;  
пароль: qwerty-100Z;  
где Z - целое число от 1 до 10.  
Пароли хранятся в таблице Users зашифрованном виде.
