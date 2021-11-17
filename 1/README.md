### Install nginx and host a simple index.html with message “hello nginx”
Steps:<br/>
Installing Nginx<br/>
<pre>sudo apt install nginx</pre> <br/>

![install](https://user-images.githubusercontent.com/53372486/141984734-26ca0f29-2121-473d-b314-23d8f3115e61.png)
<br/>
Checking nginx status<br/>
<pre>systemctl status nginx</pre> <br/>

![running nginx](https://user-images.githubusercontent.com/53372486/141984743-a0cda6bb-f201-4c37-93ac-24100e0632f2.png)
<br/>

![running nginx in web](https://user-images.githubusercontent.com/53372486/141984751-fc824c80-f856-43a7-8981-4644b2932f35.png)
<br/>

Setting Up Server Blocks<br/>
Create the directory for localhost<br/>
<pre>sudo mkdir -p /var/www/localhost/html</pre> <br/>
create a sample index.html page<br/>
<pre>nano /var/www/localhost/html/index.html</pre> <br/>
Add message in html file<br/>
<pre>hello nginx</pre>

![index html](https://user-images.githubusercontent.com/53372486/141984764-239883a7-fd96-4aad-ad75-6e1e9390e695.png)<br/>

create localhost.conf file inside /etc/nginx/sites-available<br/>
<pre>sudo nano /etc/nginx/sites-available/localhost.conf</pre> <br/>
Add below line in localhost.conf file<br/>
<pre>server {<br/>
        listen 80;<br/>
        listen [::]:80;<br/>
        root /var/www/localhost/html;<br/>
        index index.html index.htm index.nginx-debian.html;<br/>
        server_name localhost;<br/>
        location / {<br/>
                try_files $uri $uri/ =404;<br/>
        }<br/>
    }</pre>
    
<br/>
 Enable the file by creating a link which Nginx reads from during startup<br/>
<pre>sudo ln -s /etc/nginx/sites-available/localhost /etc/nginx/sites-enabled/</pre> <br/>

For testing<br/>
    <pre>sudo nginx -t</pre>   
    <br/>
Restart nginx<br/>
<pre>sudo systemctl restart nginx</pre><br/>
Display message<br/>

![display message](https://user-images.githubusercontent.com/53372486/141984772-f6075d6c-3440-4dda-8a3a-b00634fc8532.png)

