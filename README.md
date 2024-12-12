## CYBERTOOLS
basic commands for tools

## nmap
nmap - to find services open on server

* To scan the live Host
```console
nmap -sP x.x.x.1/24                 
nmap -sn x.x.x.1/24
```
* -sn: To nowa wersja składni "Ping Scan" (dawniej -sP). Oznacza "Disable Port Scanning", co znaczy, że Nmap nie wykonuje skanowania portów, a jedynie sprawdza, czy hosty są aktywne w danej podsieci.

To find the Specific open port 
```console
nmap -p port x.x.x.1/24 --open
```
To find the OS 
```console
nmap -O x.x.x.x 
```
Comprehensive Scan
```console
nmap -Pn -A x.x.x.1/24 -vv --open   
```
* -Pn
Wyłącza pingowanie hostów przed skanowaniem (oznacza: "Treat all hosts as online").
Domyślnie Nmap sprawdza, czy hosty są aktywne, wysyłając zapytania ICMP (ping) lub inne testy. Przy użyciu -Pn narzędzie zakłada, że wszystkie hosty w danym zakresie x.x.x.1/24 są dostępne i przystępuje do skanowania nawet, jeśli ping ICMP jest zablokowany przez zaporę sieciową (firewall).
* -A
Aktywuje szczegółowe skanowanie i umożliwia:
Wykrywanie systemu operacyjnego (OS Detection),
Wykrywanie usług na otwartych portach (Service Version Detection),
Śledzenie trasy (traceroute),
Pobieranie dodatkowych informacji o hostach (np. banery aplikacji).
Opcja ta jest przydatna do głębokiej analizy hostów w sieci.
* -vv
Ustawia wysoki poziom szczegółowości w wyjściu (Verbose Mode).
-vv oznacza "Very Verbose", dzięki czemu Nmap generuje więcej informacji w czasie rzeczywistym podczas wykonywania skanowania.
* --open
Wyświetla tylko hosty i porty, które są otwarte.
Ignoruje porty zamknięte lub filtrowane, aby skupić się wyłącznie na tych, które mogą świadczyć usługi lub być potencjalnie dostępne.

## netdiscover
netdiscover - to find active machines

```console
netdiscover -i eth0     
netdiscover -r x.x.x.1/24
```
* -i eth0: Określa interfejs sieciowy, na którym ma działać narzędzie, w tym przypadku eth0 (tryb pasywny)
* -r x.x.x.1/24: Określa zakres adresów IP, który ma być aktywnie skanowany (tryb aktywny)

## hydra

hydra - to bruteforce usernames and passwords.

## John The Ripper

## wpscan
wpscan - to bruteforce wordpress website (users and passwords)

## sqlmap
sqlmap - to find data (phones, usernames, etc) in database 

## adb

## hashcalc
hashcalc -  to calculate SHA1 hash

## veracrypt
veracrypt - to decrypt volume and find secret file

## BCTextEncoder
BCTextEncoder - to decode text using given secret

## Cryptool
cryptool - to decode .hex ,.dex, .oct file

## snow

## openstego

## covert_tcp
covert_tcp
