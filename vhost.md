* Allez dans /etc/apache2/sites-available/

* créer un nouveau fichier .conf (sudo nano all.conf )

* virtual host docs ubuntu (copier coller all) ou ça

```
<VirtualHost *:80>
	ServerAlias www.monsite1.fr
	DocumentRoot /var/www/monsite1
	<Directory />
		Options FollowSymLinks
		AllowOverride None
	</Directory>
	<Directory /var/www/monsite1>
		Options Indexes FollowSymLinks MultiViews
		AllowOverride None
		Order allow,deny
		allow from all
	</Directory>
</VirtualHost>
```

* faire un "a2ensite" pour activer le site.

* reload

* faire un "a2dissite" pour désactiver un site

* creer le dossier dans /var/www/ si il n'est pas créer
