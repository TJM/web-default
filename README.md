web-default
===========

Very basic virtual hosting configuration

## Initial Setup
1. Clone git repo (or install)
1. Link Scripts
    mkdir -p /root/bin && ln -s /web/DEFAULT/bin/* /root/bin/
1. Link Virtual Host Permissions file
    ln -s /web/DEFAULT/conf/y-VirtualHostPermissions.conf /etc/httpd/conf.d/
1. Run updateAllWebConfigs
    updateAllWebConfigs
1. Restart Apache
    service httpd restart
