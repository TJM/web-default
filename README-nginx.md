web-default
===========

Very basic virtual hosting configuration
 -- nginx edition

Initial Setup
-------------
Default/Global settings

NOTE: ngix is assumed to be installed via the passenger-install-nginx-module utility after installing rvm and the desired version of ruby, and "rvm use" -ing that version

* Clone git repo (or install)

```bash
mkdir /web
cd /web
git clone https://github.com/TJM/web-default DEFAULT
```

* Copy Example configs

```bash
cd /web/DEFAULT/conf
for file in *NGINX.EXAMPLE; do
  newfile=`basename $file .NGINX.EXAMPLE`
  cp $file $newfile
done

### EDIT AS NECESSARY
```

* Link Scripts

```bash
mkdir -p /root/bin && ln -s /web/DEFAULT/bin/* /root/bin/
```    

* Create conf.d and add it to the config
 * EDIT: /opt/nginx/conf/nginx.conf
  * Add "        include conf.d/*.conf;" before the last "}"

```bash
mkdir /opt/nginx/conf/conf.d
```

* Create a DEV password (used to access dev.DOMAIN.COM)

```bash
yum install -y httpd-tools
htpasswd -c /web/DEFAULT/pw/dev.pw DEVUSER
```

* Insert global SSH Keys into /web/DEFAULT/conf/authorized_keys2 (these will be automatically propagated to every website)

```bash
cat >> /web/DEFAULT/authorized_keys2
	[[paste keys in]]
	CTRL+D
```

* Run updateAllWebConfigs

```bash
updateAllWebConfigs
```

* Restart Nginx
NOTE: init scripts are not installed by default

```bash
service nginx restart
```
* Create a default website

```bash
touch website/index.html
```

Adding a new host
------------------
```bash
useradd -d /web/somedomain.com -c "somedomain.com" somedomain
updateAllWebConfigs
service httpd restart
```
(TBD)
