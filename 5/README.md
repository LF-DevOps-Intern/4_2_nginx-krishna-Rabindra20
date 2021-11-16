### Reverse proxy all http traffic of port 82 to port 85.
Steps:<br/>
create reverse_proxy1.conf file inside /etc/nginx/sites-available<br/>
<pre>sudo nano reverse_proxy1.conf</pre><br/>
Add below line in reverse_proxy1.conf file<br/>
<pre>server {<br/>
    listen 85;<br/>
    server_name localhost;<br/>
    location / {<br/>
        proxy_pass http://localhost:82/test/;<br/>
    }<br/>
}</pre><br/>

![proxy](https://user-images.githubusercontent.com/53372486/142036009-6998b7c6-9f51-428c-9522-4d0741429a17.png)<br/>

creating a link from it to the sites-enabled directory, which Nginx reads from during startup<br/>
<pre>sudo ln -rs reverse_proxy.conf ../sites-enabled/</pre><br/>
For testing<br/>
    <pre>sudo nginx -t</pre>   
    <br/>
Restart nginx<br/>
<pre>sudo systemctl restart nginx</pre><br/>

![restart](https://user-images.githubusercontent.com/53372486/142036023-35c211a0-3768-4959-9aee-a251d063edb0.png)<br/>
<br/>
Display message<br/>

![host 85](https://user-images.githubusercontent.com/53372486/142036575-b7df1158-f8d2-4205-98cc-5dfcf280473c.png)<br/>


