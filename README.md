web-default
===========

Very basic virtual hosting configuration

Initial Setup
-------------
Default/Global settings

* Clone git repo (or install)

```bash
mkdir /web
cd /web
git clone https://github.com/TJM/web-default DEFAULT
```

* Copy Example configs

```bash
cd /web/DEFAULT/conf
for file in *EXAMPLE; do
  newfile=`basename $file .EXAMPLE`
  cp $file $newfile
done

### EDIT AS NECESSARY
```

* Link Scripts

```bash
mkdir -p /root/bin && ln -s /web/DEFAULT/bin/* /root/bin/
```    

* Link Virtual Host Permissions file

```bash
ln -s /web/DEFAULT/conf/y-VirtualHostPermissions.conf /etc/httpd/conf.d/
```

* Create a DEV password (used to access dev.DOMAIN.COM)

```bash
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

* Restart Apache

```bash
service httpd restart
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
