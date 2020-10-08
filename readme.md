some bzdury

 #vi /etc/nginx/sites-enabled/items-rest.conf::::

server {
listen 443 default_server;
server_name myberniwebsite.xyz;
ssl on;
ssl_certificate /var/www/ssl/linkdokluczapub;
ssl_certificate_key /var/www/ssl/linkdokluczapryw;
real_ip_header X-Forwarded-For;
set_real_ip_from 127.0.0.1;

location / {
include uwsgi_params;
uwsgi_pass unix:/var/www/html/items-rest/socket.sock;
uwsgi_modifier1 30;
}


error_page 404 /404.html;
location = /404.html {
root /usr/share/nginx/html;
}

error_page 500 502 503 504 50x.html;
location = /50x.html {
root /usr/share/nginx/html;
}
}

server {
listen 80;
server_name myberniwebsite.xyz;
rewrite ^/(.*) https://myberniwebsite.xyz/$1 permanent;
}

