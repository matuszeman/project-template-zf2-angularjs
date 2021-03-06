ZF2 Apigility and AngularJS project template
==================================

All-in-one development vagrant box and project scaffold for ZF2 Apigility API server and AngularJS client-side applications.

You do NOT have to install anything locally on your dev machine - vagrant box should provide all tools necessary!

_Note_: There are some known improvements to make and issues to fix. Please see TODO or [github issues](https://github.com/kapitchi/project-template-zf2-angularjs/issues) list. 


What's included
---------------

__Server-side related stuff__

[ZF2](http://framework.zend.com/),
[Apigility](http://www.apigility.org/),
[PHPUnit](http://phpunit.de/)

__Client-side related stuff__

[jQuery](http://jquery.com/),
[AngularJS](https://angularjs.org/),
[UI Bootstrap](http://angular-ui.github.io/bootstrap/),
[RequireJS](http://requirejs.org/),
[Karma/Jasmine](http://karma-runner.github.io/),
[SASS](http://sass-lang.com/),
[Bootstrap 3 SASS](http://getbootstrap.com/css/#sass),
[FontCustom](http://fontcustom.com/)


Installation
============

__Clone project__

```
git clone https://github.com/kapitchi/project-template-zf2-angularjs.git myapp
```

__Vagrant up!__

```
cd myapp
vagrant up
```

__Add `myapp.local` to your local hosts file__

```
192.168.60.101 myapp.local
```

Linux: /etc/hosts  
Mac: /private/etc/hosts  
Windows: C:/Windows/System32/drivers/etc/hosts


__Build and run__

Connect to a box
```
vagrant ssh
```

Build a project
```
./bin/init-build
```

After build runs successfully you should be able to see working app on:
http://myapp.local

See other available services/links in _Bookmarks_ section.


Known issues
------------

__Symptom:__ On provisioning of vagrant box you get an error related to "ez_setup.py"

```
Error: curl https://bitbucket.org/pypa/setuptools/raw/bootstrap/ez_setup.py | python returned 1 instead of one of [0]
```

It looks like bitbucket implements download rate limit policy what makes a file sometimes not accessible.  
Related issue: https://bitbucket.org/pypa/setuptools/issue/192/any-attempt-to-download-ez_setuppy-fails

__Fix:__ Try again later. Wait for package maintainers to update dependency links.


__Symptom:__ Phpmyadmin missing table issues

__Fix:__ https://github.com/kapitchi/project-template-zf2-angularjs/issues/3


Bookmarks
=========

__Your project__

http://myapp.local


__Apigility__

http://192.168.60.101:8080/apigility/ui

_Note: Available only in development mode. See Development section below._


__PHP code coverage__

http://192.168.60.101/report/test/php/coverage/

_Note: You need to run `phpunit` first_


__JS code coverage__

http://192.168.60.101/report/test/js/coverage/

_Note: You need to run `karma` first_

__MySQL__

http://192.168.60.101/phpmyadmin  
User: root  
Pass: 123

__MySQL clients using TCP/IP over SSH__

For tools like e.g. [MySQL Workbench](http://www.mysql.com/products/workbench/) 

SSH Hostname: 192.168.60.101:22  
SSH Username: vagrant  
SSH Key file: puphpet/files/dot/ssh/id_rsa  
MySQL Hostname: 127.0.0.1  
MySQL Port: 3306  
MySQL user: root  
MySQL pass: 123  


__Mailcatcher__

http://192.168.60.101:1080/

In order to use mailcatcher your application mailer needs to be set up using this SMTP settings:  
Host: 127.0.0.1  
Port: 1025



Development
===========

_Note:_ Commands below supposed to be run on vagant box (in `/vagrant` folder) and not locally on you development machine.

Apigility Admin
---------------

Apigility Admin is devel tool and needs write permission on certain folders/files (e.g. `config/autoload/global.php`, `config/autoload/local.php`, `module` folder, etc).
Instead of messing up with write permissions on project folders it's better to run it using PHP build-in server using vagrant user.

On vagrant box run a script below.
This enables development mode, then runs Apigility using PHP build-in server and once stopped (using CTRL+C) switches development mode off again.
```
./bin/apigility
```

UI should now be accessible on:  
http://192.168.60.101:8080/apigility/ui

SASS/CSS
--------

Source folder: `asset/sass`  
Build command: `compass compile`  
Build path: `public/build/css`  


Unit testing
------------

__PHP__

Tests are under `test/php` folder.

```
phpunit
```

Code coverage
http://192.168.60.101/report/test/php/coverage/

__Javascript__

Tests are under `test/js` folder.

```
karma start
```

Code coverage
http://192.168.60.101/report/test/js/coverage/


Grunt tasks
-----------

`grunt bower` - adds bower components into RequireJS config file `public\config.js`


PHP Debugging
-------------

Find an extension for your browser here:
http://xdebug.org/docs/remote

Start listening to debug connections in your IDE, switch debug on using browser extension and refresh the page (tested with PhpStorm 7.1.3).
Note: You need to set path mapping in your IDE: your local project root folder = `/vagrant` path on vagrant box

Vagrant box
===========

Ubuntu 12.04 Precise 64bit

Box is based on https://puphpet.com/ with some extra provisioning (`puphpet/files/exec-once`).

Default configuration can be modified in /puphpet/config.yaml. This file can be uploaded to https://puphpet.com/ to be modified using an UI.

* Apache
* PHP 5.5 - xdebug
* MySQL
* mailcatcher


Modified files/folders generated by puphpet.com:

* `puphpet/files/exec-once` - some extra provisioning
* `puphpet/files/dot/.bash_aliases` - look for '#kapitchi'


TODO
====

See: https://github.com/kapitchi/project-template-zf2-angularjs/issues

* grunt-ify project
* replace provisioning shell scripts with puppet stuff
* Advanced Rest Client example settings
* docs generation
* apigility server (grunt) command
* set PHP to use mailcatcher

__To consider__

* https://www.npmjs.org/package/grunt-vagrant-ssh
* https://github.com/btford/ngmin
* http://mobileangularui.com/


Contributing
============

Please contact me on matus.zeman@gmail.com with any comments/feedback/ideas.


__Maintaining__

Things to watch to keep this up-to-date:

* Apigility skeleton app - https://github.com/zfcampus/zf-apigility-skeleton


License
=======

[The MIT License (MIT)](https://github.com/kapitchi/project-template-zf2-angularjs/blob/master/LICENSE)