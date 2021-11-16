### What are nginx header security and its uses. And also implement in the test.conf file.
Steps:<br/>
create localhost.conf file inside /etc/nginx/sites-available<br/>
<pre>sudo nano localhost.conf</pre><br/>
Add below line in localhost.conf<br/>
<pre>server {<br/>
        listen 80;<br/>
       # listen [::]:80;<br/>
        root /var/www/localhost/html;<br/>
        index index.html index.htm index.nginx-debian.html;<br/>
        server_name localhost;<br/>
        location / {<br/>
                try_files $uri $uri/ =404;<br/>
        }<br/>
        access_log /var/log/nginx/test.log;<br/>
        error_log /var/log/nginx/test-error.log;<br/>
        # Some security headers.<br/>
        add_header Referrer-Policy "strict-origin";<br/>
        add_header X-XSS-Protection "1; mode=block";<br/>
        add_header X-Frame-Options "SAMEORIGIN";<br/>
        add_header X-Content-Type-Options nosniff;<br/>

}</pre>
<br/>

![localhost conf](https://user-images.githubusercontent.com/53372486/142030766-101414d4-2f83-4a83-ae33-879baef30432.png)<br/>

creating a link from it to the sites-enabled directory, which Nginx reads from during startup<br/>
<pre>sudo ln -rs localhost.conf ../sites-enabled/</pre><br/>
For testing<br/>
    <pre>sudo nginx -t</pre>   
    <br/>

![check error](https://user-images.githubusercontent.com/53372486/142030777-8a06f67b-7124-440f-b180-c50b7409d498.png)<br/>

Restart nginx<br/>
<pre>sudo systemctl restart nginx</pre><br/>
<pre>sudo systemctl status nginx</pre><br/>

![status](https://user-images.githubusercontent.com/53372486/142030784-0cebe88e-e51f-4544-9248-0c3dd61192bf.png)<br/>

Display<br/>
open web browser > inspect > click on network > check header response<br/>

![response header](https://user-images.githubusercontent.com/53372486/142030790-03022c4a-aa9d-4b8f-a267-ef5966d9bfbc.png)
