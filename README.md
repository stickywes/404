# Spooky default Apache Welcome

This was a 404 page originally created for netmagazine.com by Hakim El Hattab! 

[Check out the demo](http://hakim.se/experiments/html5/404) or see how it looked in context on [netmagazine.com](http://hakim.se/experiments/html5/404/netmag.html).

It was subsequently modified for use as an Apache fallback page to replace the default Apache
index page on CentOS installs.

# License

MIT licensed

Copyright (C) 2011 Hakim El Hattab, http://hakim.se

Modified by Weston Wedding, http://www.westonwedding.com


# Usage

Modify your fallback page configuration.  On CentOS 7 it was `/etc/httpd/conf.d/welcome.conf`
You will need to poke around to see how your particular distribution does it.  It might not have a welcome page!

The paths in this example assume you've put this into "/var/www/html/no-index-fallback," make sure you make
modifications to adjust for your particular config.

```
# 
# This configuration file enables the default "Welcome" page if there
# is no default index page present for the root URL.  To disable the
# Welcome page, comment out all the lines below. 
#
# NOTE: if this file is removed, it will be restored on upgrades.

<LocationMatch "^/+$">
    Options -Indexes
    ErrorDocument 403 /.noindex.html
</LocationMatch>

#<Directory /usr/share/httpd/noindex>
#    AllowOverride None
#    Require all granted
#</Directory>

#Alias /.noindex.html /usr/share/httpd/noindex/index.html
#Alias /noindex/css/bootstrap.min.css /usr/share/httpd/noindex/css/bootstrap.min.css
#Alias /noindex/css/open-sans.css /usr/share/httpd/noindex/css/open-sans.css
#Alias /images/apache_pb.gif /usr/share/httpd/noindex/images/apache_pb.gif
#Alias /images/poweredby.png /usr/share/httpd/noindex/images/poweredby.png

<Directory /var/www/html/no-index-fallback>
    AllowOverride None
    Require all granted
</Directory>

Alias /.noindex.html /var/www/html/no-index-fallback/index.html
Alias /noindex/css/reset.css /var/www/html/no-index-fallback/css/reset.css
Alias /noindex/css/404.css /var/www/html/no-index-fallback/css/404.css
Alias /noindex/css/main.css /var/www/html/no-index-fallback/css/main.css
Alias /noindex/js/404.js /var/www/html/no-index-fallback/js/404.js
```
This example commented out the previous configuration and kept it around for context.  
Those Alias lines are important, don't leave them out!
