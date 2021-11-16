### Nginx Reverse proxy all http requests to nodes js api.
Steps:<br/>
Start Pm2<br/>
<pre>sudo pm2 start 6080.js</pre><br/>
create reverse_proxy.conf file inside /etc/nginx/sites-available<br/>
<pre>sudo nano reverse_proxy.conf</pre><br/>
Add below line in reverse_proxy.conf file<br/>
<pre>server {
    listen 81;
    server_name localhost;

    location / {
        proxy_pass http://localhost:6080;
    }
}</pre><br/>
![reverse conf](https://user-images.githubusercontent.com/53372486/142033450-b07582b6-6d63-44ba-a5a5-11034bc92164.png)<br/>
creating a link from it to the sites-enabled directory, which Nginx reads from during startup<br/>
<pre>sudo ln -rs reverse_proxy.conf ../sites-enabled/</pre><br/>
For testing<br/>
    <pre>sudo nginx -t</pre>   
    <br/>
Restart nginx<br/>
<pre>sudo systemctl restart nginx</pre><br/>

![restart](https://user-images.githubusercontent.com/53372486/142033465-747de75a-ca82-4c61-baf3-ab3fcb26202e.png)<br/>
<br/>
Display message<br/>

![localhost81](https://user-images.githubusercontent.com/53372486/142033473-ce682268-dc2b-4899-a7e0-fb65826d7945.png)<br/>
