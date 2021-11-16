### Create a test2.conf and listen on port 82 and  to “ location /test/” with message “ test is successful”.
Setting Up Server Blocks<br/>
Create the directory for localhost<br/>
<pre><pre>sudo mkdir -p /var/www/localhost/html/test</pre> <br/>
create a sample index.html page<br/>
nano /var/www/localhost/html/test/index.html</pre> <br/>
<html><br/>
    <head><br/>
        <title>Welcome to  nginx test</title><br/>
    </head><br/>
    <body><br/>
        <h1>test is successful</h1><br/>
    </body><br/>
</html><br/>
<br/>

![index](https://user-images.githubusercontent.com/53372486/142034066-85147676-be29-4f6f-84e9-2cc8cc6e6f18.png)<br/>
create a server block<br/>
<pre>sudo nano /etc/nginx/sites-available/test.conf</pre> <br/>
Add below line in test.conf<br/>
<pre>server {<br/>
        listen 82;<br/>
        #listen [::]:80;<br/>
         root /var/www/localhost/html;<br/>
        index index.html index.htm index.nginx-debian.html;<br/>
        server_name localhost;<br/>
        location /test/ {<br/>
        index index.html;<br/>
        #location / {<br/>
         #       try_files $uri $uri/ =404;<br/>
        }<br/>
}</pre> 
<br/>

![test conf](https://user-images.githubusercontent.com/53372486/142034857-2ecc092d-bcc9-44a9-9775-2f5900a72f35.png)<br/>

 Enable the file by creating a link which Nginx reads from during startup<br/>
<pre>sudo ln -s /etc/nginx/sites-available/localhost /etc/nginx/sites-enabled/</pre> <br/>
<pre>sudo nano /etc/nginx/nginx.conf</pre> <br/>
For testing<br/>
    <pre>sudo nginx -t</pre>   
    <br/>
Restart nginx<br/>
<pre>sudo systemctl restart nginx</pre><br/>

![restart](https://user-images.githubusercontent.com/53372486/142034074-d30b23c0-d09d-4bdf-9b41-73d3f81f090f.png)<br/>
Display message<br/>

![host in 82](https://user-images.githubusercontent.com/53372486/142034065-f5876929-5288-41e5-93f9-6070678c45f7.png)


      

