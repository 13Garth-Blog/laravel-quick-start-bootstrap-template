# Laravel quick start bootstrap template with Standard AUTH
My personal favorite clean slate Laravel CLI quick start guide.<br>
Please remember these are my personal prefrences, there are many ways to setup different laravel projects. And I get this information from :<br>
- 1: Personal Dev Experience in my career
- 2: Online research

## Prerequisite

You must have composer PHP package manager already installed on your machine.
  - If you don't have composer. Go install it. Just google composer PHP or try the links below :
      - Composer official website: https://getcomposer.org/
      - For Windows download the .exe from Composer official website
      - For mac you can use "homebrew cli" : https://brew.sh/
      - For linux you can try these cli commands :
        - ```
          sudo apt update
          sudo apt install php-cli unzip -y
          curl -sS https://getcomposer.org/installer -o composer-setup.php
          HASH="$(curl -sS https://composer.github.io/installer.sig)"
          php -r "if (hash_file('sha384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
          sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
          rm composer-setup.php
          composer -V
          ```
---
## CLI Process

Just use one of these lines for the relevant version of Laravel you want.
```
// Exampkle 1 : 
composer create-project --prefer-dist laravel/laravel blog "11.*"

// Exampkle 2 : 
composer create-project --prefer-dist laravel/laravel blog "10.*"

// Exampkle 3 : 
composer create-project --prefer-dist laravel/laravel blog "9.*"
```

The next step is to generate your starter UI. (Note, running these commands 1 at a time has better success rate without any issues) : 
```
composer require laravel/ui --dev
php artisan ui bootstrap --auth
npm install 
npm run build
```

## Uploading your js build to the server

If you using git and working locally and using laravel vite.
Build your project and use the below gitignore. This will push your build to the server.

The below is that if you don’t include certain directories then your build files will not get uploaded and some servers don’t have suffucient resources to run builds online.
So you need to build locally and upload the build via GIT.
```
/vendor/
npm-debug.log
yarn-error.log
public/hot
public_html/storage
public_html/hot
public/robots.txt
storage/*.key
.env
.htaccess
Homestead.yaml
Homestead.json
/.vagrant
.phpunit.result.cache
```

## Issues with Laravel root directory displaying instead of loading website

This has been a common issue sometimes when creating new Laravel projects for me. And this an optional extra if you need it.<br>
In the root of your project, create a .htaccess file. Then add the code below. This should redirect your project root to the public directory. 
If it doesn't work for you. Just google **"Laravel redirect root to public directory"**
```
<IfModule mod_rewrite.c>
    RewriteEngine On

    # Redirect everything to the public directory
    RewriteCond %{REQUEST_URI} !^/public/
    RewriteRule ^(.*)$ /public/$1 [L,QSA]

    # Ensure directory listing is disabled
    Options -Indexes
</IfModule>
```
