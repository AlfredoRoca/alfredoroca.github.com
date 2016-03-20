---
layout: post
title: "Nginx server config by direct IP instead domain server"
description: ""
category: [nginx, configuration]
tags: []
---
{% include JB/setup %}

# How to configure nginx server to redirect rails app without domain name

    /etc/nginx/conf.d/shk.conf 

    server {    
            client_max_body_size 20M;    
            client_body_temp_path /var/www/uploads_temp;    
            listen    46.101.186.164:80;    
            server_name  46.101.186.164;    
            root         /var/www/shk;

            location / {            
                    proxy_pass_header Server;    
                    proxy_temp_path /tmp/nginx 1 2;
                    proxy_set_header  X-Real-IP  $remote_addr;    
                    proxy_set_header  X-Forwarded-For $proxy_add_x_forwarded_for;    
                    proxy_set_header Host $http_host;    
                    proxy_set_header X-FORWARDED-PROTO $scheme;    
                    proxy_redirect off;    
                    proxy_pass http://localhost:3000;    
                    break;    
            }

            location /monit/ {            
                    proxy_set_header Host $host;    
                    proxy_set_header  X-Real-IP  $remote_addr;    
                    proxy_set_header  X-Forwarded-For $proxy_add_x_forwarded_for;    
                    proxy_pass http://localhost:2812;    
                    proxy_redirect off;    
                    rewrite ^/monit/(.*) /$1 break;    
                    proxy_ignore_client_abort on;    
            }

            error_page 503 @503;    
            # Return a 503 error if the maintenance page exists.    
            if (-f /var/www/shk/shared/public/system/maintenance.html) {      
                    return 503;    
            }
            
            location @503 {      
                # Serve static assets if found.      
                if (-f $request_filename) {        
                    break;    
                }
                # Set root to the shared directory.      
                root /var/www/shk/shared/public;    
                rewrite ^(.*)$ /system/maintenance.html 
                break;    
            }      
    }

