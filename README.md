# Nginx Proxy Inverso


### Configurar Nginx como balanceador de carga.

En el upstream configurar el cluster de servidores, con las ips internas y sus puertos si fuera necesario, en el default.conf

  upstream miprojecto {  
    server WWW.XXX.YYY.ZZZ:1234;  
    server WWW.XXX.YYY.ZZZ:1235;  
    server WWW.XXX.YYY.ZZZ:1236;  
    server WWW.XXX.YYY.ZZZ:1237;  
  }  
  
  server {  
    listen 80;  
    server_name miwebsite.com;  
    location / {  
        proxy_pass http://miprojecto;  
        proxy_set_header Host $host;  
        proxy_set_header X-Real-IP $remote_addr;  
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;  
        proxy_set_header X-Forwarded-Host $server_name;  
  
    }  
    error_page  404  /errorPages/404.html;  
  }  
  

```
conf.d/default.conf
```
