Nginx Cheat Sheet
=================
`< Blog <../blog.html>`_

A quick reference to Nginx

Created on: 2019-12-03

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



Source
------

