### What are nginx header security and its uses. And also implement in the test.conf file.
->The HTTP headers in NGINX are split in two parts: the input request headers (headers_in structure) and the output request headers (headers_out structure). There is no such an entity as a response, all the data is stored in the same single request structure. The actual response data is constructed from the request data and the headers_out structure fields.<br/>
Nowadays too many data breaches are happening, many websites are hacked due to misconfiguration or lack of protection. These security headers will protect your website from some common attacks like XSS, code injection, clickjacking, etc.<br/>

some header security are:-<br/>
1. Cross-Site Scripting Protection (X-XSS)<br/>
 ->X-XSS header helps protect websites against script injection attacks. When an attacker injects malicious JavaScript code into an HTTP request for accessing confidential information such as session cookies, at that time HTTP X-XSS-Protection header can stop the browsers from loading suce web pages, whenever any detect is reflected cross-site scripting (XSS) attacks. XSS is a very common and effective attack.<br/>
   <pre>X-XSS-Protection: 0 <br/>
   X-XSS-Protection: 1 <br/>
   X-XSS-Protection: 1; mode=block <br/>
   X-XSS-Protection: 1; report=<reporting-uri></pre>
  <br/>

2. Website IFrame Protection<br/>
 ->The X-Frame-Options HTTP response header can be used to instruct the browser whether a web page should be allowed to render a <frame>, <iframe>, <embed> or <object> element on website or not.<br/>
  <pre>X-Frame-Options: DENY <br/>
  X-Frame-Options: SAMEORIGIN</pre>
  <br/>

3. Preventing Content-Type Sniffing<br/>
 ->X-Content-Type-Options response header prevents the browser from MIME-sniffing a response away from the declared content-type.<br/>
  <pre>X-Content-Type-Options: nosniff </pre><br/>

4. Content Security Policy<br/>
 ->Content-Security-Policy header is used to instruct the browser to load only the allowed content defined in the policy.<br/>
<pre>Content-Security-Policy: <policy-directive>; <policy-directive></pre><br/>

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

}
</pre>
<br/>

![localhost conf](https://user-images.githubusercontent.com/53372486/142030766-101414d4-2f83-4a83-ae33-879baef30432.png)<br/>

creating a link from it to the sites-enabled directory, which Nginx reads from during startup<br/>
<pre>sudo ln -rs /etc/nginx/sites-available/localhost.conf /etc/nginx/sites-enabled/</pre><br/>
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
