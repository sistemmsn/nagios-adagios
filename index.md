## Adagios para mortales

Pasos para la instalacion de adagios de manera correcta

### Requerimiento


```
# Header 1

rpm -ihv http://opensource.is/repo/ok-release.rpm \
	&& rpm -Uvh https://labs.consol.de/repo/stable/rhel7/x86_64/labs-consol-stable.rhel7.noarch.rpm \
	&& yum update -y ok-release
 
yum --enablerepo=ok-testing install -y  git adagios okconfig acl python-setuptools postfix python-pip mod_wsgi 


- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
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


```
#Agregamos los parametros de configuracion 
4.    sed -i 's|etc/nagios/nagios.cfg|usr/local/nagios/etc/nagios.cfg|'  /etc/okconfig.conf && \
      sed -i 's|/etc/nagios/nagios.cfg|/usr/local/nagios/etc/nagios.cfg|'  /etc/adagios/adagios.conf && \
      sed -i 's|/usr/share/nagios/html/pnp4nagios/index.php|/usr/local/pnp4nagios/share/index.php|'  /etc/adagios/adagios.conf && \
      sed -i 's|/etc/nagios/adagios/|/usr/local/nagios/etc/adagios/|'  /etc/adagios/adagios.conf && \
      sed -i 's|/usr/sbin/nagios|/usr/local/nagios/bin/nagios|'  /etc/adagios/adagios.conf  && \
      sed -i 's|None|"/usr/local/nagios/var/rw/live"|'  /etc/adagios/adagios.conf && \


```
### Realizamos la verificacion:


``` 
5.    okconfig init && okconfig verify

```

Para mas detalles [pagina official](http://adagios.org/).

### Realizamos la verificacion

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/sistemmsn/nagios-adagios/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
