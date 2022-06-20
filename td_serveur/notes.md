# TD serveur notes

## Utilisateur apache

Utilisateur apache present  

```shell
ps -aux | grep apache
```

On a root car le service main a besoin de root  

c'est www-data qui contient apache

## Retirer ServerTokens

Dans /etc/conf-available/security.conf :

```bash
ServerTokens Prod
ServerSignature off

$ systemctl reload apache2
```

## Empecher d'accéder à tout les services

Rajouter

```bash
    Options -Indexes
```

Le - indique on enlève l'option
Dans Notre Directory /var/www/

## Autoriser .htaccess

Option FileInfo dans AllowOverride de apache2.conf

Exemple de réecriture

```bash
RewriteRule "script/(.+)/(.+)$" "/script?param1=$1&param2=$2"
RewriteRule "script/([a-z0-9]+)/([a-z0-9]+)$" "/script?param1=$1&param2=$2"
```

Le $ permet de dire fin de regex pour éviter les soucis

## Par conf apache

Dans notre virtualhost

```bash
<Directory /var/www/html>
Conf de apache2.conf
RewriteEngine On
RewriteRule "script/([a-z0-9]+)/([a-z0-9]+)$" "/script?param1=$1&param2=$2"
</Directory>
```