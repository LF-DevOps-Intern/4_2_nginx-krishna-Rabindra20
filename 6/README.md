### Install LEMP stack (avoid installing mysql) and open info.php on port 80 and print message  info.php.
Steps:<br/>
Install php<br/>
<pre>sudo apt install php-fpm</pre><br/>

![install php](https://user-images.githubusercontent.com/53372486/142132079-7e9fe600-128c-421d-bd8d-1289971f1a97.png)<br/>

No need to install mysql<br/>
Create the directory for localhost<br/>
<pre>sudo mkdir -p /var/www/php</pre> <br/>
create a sample info.php page<br/>
<pre>nano /var/www/php/info.php</pre> <br/>
Add message in php file<br/>
<pre><?php<br/>
phpinfo();<br/>
?><br/></pre>

![php](https://user-images.githubusercontent.com/53372486/142132086-0117930c-d5c7-4f5e-a0d4-18848c74c9f8.png)
<br/>

create php.conf file inside /etc/nginx/sites-available<br/>
<pre>sudo nano /etc/nginx/sites-available/php.conf</pre> <br/>
Add below line in php.conf file<br/>
<pre>server {<br/>
        listen 80;<br/>
        root /var/www/html;<br/>
        index index.php index.html index.htm index.nginx-debian.html;<br/>
        server_name your_domain;<br/>
        location / {<br/>
                try_files $uri $uri/ =404;<br/>
        }<br/>
        # This location block handles the actual PHP processing by pointing Nginx to the fastcgi-php.conf configuration file and the php7.2-fpm.sock file, which declares what socket is associated with php-fpm.<br/>
        location ~ \.php$ {<br/>
                include snippets/fastcgi-php.conf;<br/>
                fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;<br/>
        }<br/>
        #The last location block deals with .htaccess files, which Nginx does not process. By adding the deny all directive, if any .htaccess files happen to find their way into the document root they will not be served to visitors.<br/>
        location ~ /\.ht {<br/>
                deny all;<br/>
        }<br/>
}<br/></pre>

   ![php conf](https://user-images.githubusercontent.com/53372486/142135526-f119b82d-4456-4457-b979-31a47ef689c9.png)
 <br/>

 Enable the file by creating a link which Nginx reads from during startup<br/>
<pre>sudo ln -rs /etc/nginx/sites-available/php.conf /etc/nginx/sites-enabled/</pre> <br/>

![symlink](https://user-images.githubusercontent.com/53372486/142132092-af16420e-044f-4421-8e4e-d61e044f2bd4.png)<br/>

For testing<br/>
    <pre>sudo nginx -t</pre>   
    <br/>

![test](https://user-images.githubusercontent.com/53372486/142132097-c5c71c60-7137-4941-be44-3fd97be33de6.png)<br/>

Restart nginx<br/>
<pre>sudo systemctl restart nginx</pre><br/>
Display message<br/>

![80running](https://user-images.githubusercontent.com/53372486/142132075-7aaf83f9-992b-4796-b203-06a54c97268e.png)<br/>


