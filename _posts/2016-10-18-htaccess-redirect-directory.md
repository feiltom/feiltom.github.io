---
layout: post
title: Htaccess redirection domaine vers repertoire 
subtitle: Exemple avec un NDD imaginaire
---
    
    RewriteEngine on
    RewriteCond %{HTTP_HOST} ^(www.)?feiltom.fr$
    RewriteCond %{REQUEST_URI} !^/feiltom_fr/
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule ^(.*)$ /feiltom_fr/$1
    RewriteCond %{HTTP_HOST} ^(www.)?feiltom.fr$
    RewriteRule ^(/)?$ feiltom_fr/index.php [L]
    
    RewriteCond %{HTTP_HOST} ^(www.)?feiltom.es$
    RewriteCond %{REQUEST_URI} !^/feiltom_es/
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule ^(.*)$ /feiltom_es/$1
    RewriteCond %{HTTP_HOST} ^(www.)?feiltom.es$
    RewriteRule ^(/)?$ feiltom_es/index.php [L]
    
    RewriteCond %{HTTP_HOST} ^(www.)?feiltom.com$
    RewriteCond %{REQUEST_URI} !^/feiltom_gb/
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule ^(.*)$ /feiltom_es/$1
    RewriteCond %{HTTP_HOST} ^(www.)?feiltom.com$
    RewriteRule ^(/)?$ feiltom_gb/index.php [L]
