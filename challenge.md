 **on installe Apache comme serveur web :** 
```
 sudo apt update && sudo apt install apache2 -y  
sudo systemctl enable --now apache2
```
**on Configure les logs sur le fichier apache :**
```
nano ../etc/apache2/apache2.conf
```
```
LogFormat "%h %l %u %t \"%r\" %>s %b" common
CustomLog ${APACHE_LOG_DIR}/access.log common
ErrorLog ${APACHE_LOG_DIR}/error.log
```
```
sudo systemctl restart apache2
```
**on Génére un trafic :**
```
curl -I http://localhost/  ----> renvoie code 200
curl -I http://localhost/notfound ---> renvoie un erreur 404
```
Sur le navigateur : http://192.168.1.130/

**on Analyse les logs :**
```
grep ' 200 ' /var/log/apache2/access.log
grep ' 404 ' /var/log/apache2/access.log
awk '{print $1}' /var/log/apache2/access.log | sort | uniq -c | sort -nr | head -10
192.168.1.110 - - [10/Mar/2025:10:47:12 +0100] "GET /index.html HTTP/1.1" 200 512
```
