web-default
===========

Very basic virtual hosting configuration

## Initial Setup
Default/Global settings
1. Clone git repo (or install)
1. Link Scripts
	mkdir -p /root/bin && ln -s /web/DEFAULT/bin/* /root/bin/
    
1. Link Virtual Host Permissions file
	ln -s /web/DEFAULT/conf/y-VirtualHostPermissions.conf /etc/httpd/conf.d/

1. Create a DEV password (used to access dev.DOMAIN.COM)
	htpasswd -c /web/DEFAULT/pw/dev.pw DEVUSER

1. Insert SSH Keys into /web/DEFAULT/conf/authorized_keys2 (these will be automatically propagated to every website)
	cat >> /web/DEFAULT/authorized_keys2
	[[paste keys in]]
	CTRL+D

1. Run updateAllWebConfigs
	updateAllWebConfigs
    
1. Restart Apache
	service httpd restart

1. Create a default website
	touch website/index.html

## Adding a new host
	useradd -d /web/somedomain.com -c "somedomain.com" somedomain
	updateAllWebConfigs
	service httpd restart
(TBD)
