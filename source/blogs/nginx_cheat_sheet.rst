Nginx Cheat Sheet
=================
`< Blog <../blog.html>`_

A quick reference to Nginx

Created on: 2019-12-03

Tag: `cheat_sheet <tag_cheat_sheet.html>`_

.. warning:: under heavy construction and not well organized

access and error log
--------------------
by default nginx access log can be found at::

    /var/log/nginx/access.log

and the error log at::

    /var/log/nginx/error.log


nginx trim the .html
--------------------
https://stackoverflow.com/a/38238001/5350059

https://serverfault.com/questions/514044/nginx-is-cutting-the-end-of-dynamic-pages-and-caching-them

custom 404
----------
https://www.digitalocean.com/community/questions/404-error-page-instead-of-default-nginx-welcome-page
https://serverfault.com/questions/354803/nginx-custom-404-error-page-for-virtual-host

reverse proxy
-------------
reverse proxy config::

    http {
        server {
            listen 80;
            server_name foo.com;

            location /service1/ {
                proxy_pass http://$IP:PORT/;
            }

            location /service2/ {
                proxy_pass http://$IP:PORT/;
            }

        }
    } 

source: https://stackoverflow.com/a/42452204/5350059

simple reverse proxy with ssl
-----------------------------
simple reverse proxy with ssl::

   server {
    listen 80;
    return 301 https://$host$request_uri;
    }

    server {

        listen 443;
        server_name sub.domain.com;

        ssl_certificate           /etc/nginx/cert.crt;
        ssl_certificate_key       /etc/nginx/cert.key;

        ssl on;


        location / {
          proxy_pass          http://localhost:8080;
        }
    }

source: https://www.digitalocean.com/community/tutorials/how-to-configure-nginx-with-ssl-as-a-reverse-proxy-for-jenkins

replace or remove subdirectory in reverse proxy
-----------------------------------------------
to replace or remove subdirectory in reverse proxy::

   location /site1/ {
        proxy_pass http://localhost:8081/;
        # ... more config ... #
    }

notice the tailing `/` both after the `site` and `http://localhost:8081`

source: https://serverfault.com/a/444753/

Source
------

