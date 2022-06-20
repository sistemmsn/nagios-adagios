## Adagios para mortales

Pasos para la instalacion de adagios de manera correcta

### Requerimiento


```
# by sistemmsn

rpm -ihv http://opensource.is/repo/ok-release.rpm \
	&& rpm -Uvh https://labs.consol.de/repo/stable/rhel7/x86_64/labs-consol-stable.rhel7.noarch.rpm \
	&& yum update -y ok-release
 
yum --enablerepo=ok-testing install -y  git adagios okconfig acl python-setuptools postfix python-pip mod_wsgi 

```

### Una vez instalado los requerimientos:

```
1. cd  /usr/local/nagios/etc

2.  git init /usr/local/nagios/etc
    git config user.name "admin"
    git config user.email "admin@adagios.local"
    git add . 
    git commit -a -m "Initial commit"

```

```

3.  mkdir -p /usr/local/nagios/etc/adagios
	    pynag config --append cfg_dir=/usr/local/nagios/etc/adagios
   
```

#Agregamos los parametros de configuracion

```

 
4.    sed -i 's|etc/nagios/nagios.cfg|usr/local/nagios/etc/nagios.cfg|'  /etc/okconfig.conf && \
      sed -i 's|/etc/nagios/nagios.cfg|/usr/local/nagios/etc/nagios.cfg|'  /etc/adagios/adagios.conf && \
      sed -i 's|/usr/share/nagios/html/pnp4nagios/index.php|/usr/local/pnp4nagios/share/index.php|'  /etc/adagios/adagios.conf && \
      sed -i 's|/etc/nagios/adagios/|/usr/local/nagios/etc/adagios/|'  /etc/adagios/adagios.conf && \
      sed -i 's|/usr/sbin/nagios|/usr/local/nagios/bin/nagios|'  /etc/adagios/adagios.conf  && \
      sed -i 's|None|"/usr/local/nagios/var/rw/live"|'  /etc/adagios/adagios.conf && \
      sed -i 's|/etc/nagios/passwd|/usr/local/nagios/etc/htpasswd.users|'  /etc/httpd/conf.d/adagios.conf 

```
- Nota en este proceso tienen que tener el livestatus configurado antes de realizar la verificacion

### Realizamos la verificacion:


``` 
5.    okconfig init && okconfig verify

6.    Reiniciamos el apache y listo.
```

- Nota en el OKconfig requiere de otras configuraciones eso lo realizare despues 


Para mas detalles [pagina official](http://adagios.org/).