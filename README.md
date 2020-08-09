1 - In order for captive portal to work,  make sure you have simcard inserted, or bluetooth data is connected with phone,  because it needs data packets to receive, 
2 - Remember that your hotspot ip address  by default is-      192.168.43.1
3 - Remember that port 8080 runs on your ip address, so basically now it ip address and port adds up-
                  192.168.43.1:8080
4 - Remember that what we are doing here is host our file in 8080 port then redirecting users into port 80 -
( Port 80 is also callled as 192.168.43.1, means that 80 port actually is the port of ip itself )

5 - You need the webhost app ,  here i have "Ksweb" with package name as "ru.kslabs.ksweb-1"
/OR/ "bit webserver" with package name as "com.andi.serverweb_2.4.2_paid-www.apkhere.com"


Ofc you need rooted device. I am using lenovo a6000.
_________________________________________________
¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤
Make sure to start the hotspot,  then click on 'Webserver'  button  to start "bit server"/"KSweb"  app running in the background in port 8080 , 
Then follow the steps  6 and 7. -- 
Step 6 and 7 are for KSWEB and BIT SERVER , you just have to follow one of them -
_________________________________________________
¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤
6 - For " KSWEB app "'

¤ Slide and go to Settings , Then allow "root" 
¤ After that slide to find LIGHTTPD and click on "Configuration - Edit "
¤ Now edit the configuration .
We simply have to add 3 lines here - 

server.document-root = "/sdcard/www" 
server.error-handler-404 = "/404.php"
server.dir-listing = "disable"

(server.document-root = "/sdcard/www"  -- This line is already present in line 11,  so change to /sdcard/www)
(second line i added in line 31)
( I added third line at line 32)

7 - ¤ After that you can go to the root folder of ksweb to check "lighttpd.confg" , if it is saved successfully and if not then change it there -

/data/data/com.andi.serverweb/files/lighttpd

¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤
_________________________________________________
 6 - FOR "BIT SERVER APP".

Open " settings "  in " bit server app" . After that - Go to lightpadd configuration , edit them and make them like this below,  it should look like this- (these are 5 to 10 lines only )  

server.document-root = "/sdcard/www/"
dir-listing.activate = "enable"
server.errorlog = "/sdcard/wwwconf/server.log"
server.pid-file = "/data/user/0/com.andi.serverweb/files/tmp/lighttpd.pid"
server.error-handler-404 = "/404.php"
server.dir-listing = "disable"

¤ Check the screenshot for more. ¤

7 - After that open root explorer /mixplorer and go to the directory of - 
 /data/data/com.andi.serverweb/files/lighttpd/lighttpd.conf

¤  - Under lighttpd.conf , check again that this line should look like this-

server.document-root = "/sdcard/www/"
dir-listing.activate = "enable"
server.errorlog = "/sdcard/wwwconf/server.log"
server.pid-file = "/data/user/0/com.andi.serverweb/files/tmp/lighttpd.pid"
server.error-handler-404 = "/404.php"
server.dir-listing = "disable"

This line changes automatically many times when we restart the "bit server" , so make sure that it becomes  this - 

server.document-root = "/sdcard/www/"
_______________________________________________
¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤

8 -  Put "404.php" and  "splash" folder into /sdcard/www  (www folder) 
(because 80 port gonna run at our ip address which is 192.168.43.1:8080 ; remember that 8080 is port number here).

9 - After that open " ip2 app" , here execute these codes one after another. 
(After trying i found that u can execute them all at once too after coping) 

iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8080
iptables -A FORWARD -p udp --dport 53 -j ACCEPT
iptables -A FORWARD -p udp --sport 53 -j ACCEPT
iptables -t nat -A PREROUTING -p tcp --dport 80 -j DNAT --to-destination 192.168.43.1:8080
iptables -P FORWARD DROP




