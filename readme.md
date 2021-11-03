Deploying a Laravel App via Elastic Beanstalk | Amazon Web Services BASICS
==========================================================================

* ***Actions on the deployment of the project:***

- Making a new project aws-laravel_academind.loc:

	sudo chmod -R 777 /var/www/LARAVEL/AWS/aws-laravel_academind.loc

	//!!!! .conf
	sudo cp /etc/apache2/sites-available/test.loc.conf /etc/apache2/sites-available/aws-laravel_academind.loc.conf
		
	sudo nano /etc/apache2/sites-available/aws-laravel_academind.loc.conf

	sudo a2ensite aws-laravel_academind.loc.conf

	sudo systemctl restart apache2

	sudo nano /etc/hosts

	cd /var/www/LARAVEL/AWS/aws-laravel_academind.loc

- Deploy project:

	`git clone << >>`
	
	`or Download`
	
	_+ Сut the contents of the folder up one level and delete the empty one._

	`composer install`	

---

Academind

[Deploying a Laravel App via Elastic Beanstalk | Amazon Web Services BASICS (28:07)]( https://www.youtube.com/watch?v=ISVaMijczKc&ab_channel=Academind )

Elastic Beanstalk is a great service to get your web application into the web. This video shows how you can easily use it to deploy a Laravel application which even uses a database!

Want to learn AWS Serverless apps? Dive into my complete introduction: 
<https://acad.link/aws-serverless>

The sample project: 
<https://github.com/academind/laravel-simple-blog>
	
Get Composer (for installing dependencies): 
<https://getcomposer.org/>

More on .ebextensions: 
<https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/ebextensions.html>

Dive into the EB CLI: 
<https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3.html>

Elastic Beanstalk Pricing: 
<https://aws.amazon.com/ru/elasticbeanstalk/pricing/>

Other useful AWS Articles:
	
- Getting Started: 
<https://aws.amazon.com/getting-started>

- Infrastructure: 
<https://aws.amazon.com/ru/about-aws/global-infrastructure/>

- Pricing: 
<https://aws.amazon.com/pricing>

Want to become a frontend developer? Consider diving into some of my courses:

Angular vs React vs Vue - Quickstart and Comparison: 
<https://acad.link/ng-vs-react-vs-vue>

Ionic + Angular - The Practical Guide: 
<https://acad.link/ionic>

Angular - The Complete Guide: 
<https://acad.link/angular>

Vue.js - The Complete Guide: 
<https://acad.link/angular>

[(1:35)]( https://youtu.be/ISVaMijczKc?t=95 ) `EC2`.

[(2:05)]( https://youtu.be/ISVaMijczKc?t=125 ) `Elastic Beanstalk`.

[(2:50)]( https://youtu.be/ISVaMijczKc?t=170 ) `laravel-academind-blog`

`Create Application`.

![screenshot of sample]( https://github.com/mslobodyanyuk/aws-laravel_academind/blob/main/public/images/aws/1.png )

[(3:10)]( https://youtu.be/ISVaMijczKc?t=190 ) 

_"The zip file which you Upload here should contain all the source files and NOT a folder which contains all the source files."_

`Extract archive`.

_"In this folder `Select` all the files and `Compress` them, `zip` them again."_

[(3:25)]( https://youtu.be/ISVaMijczKc?t=205 ) Edit `.env`.

```
APP_ENV=production
```

[(5:00)]( https://youtu.be/ISVaMijczKc?t=300 )

	composer install

[(5:30)]( https://youtu.be/ISVaMijczKc?t=330 ) Generate `APP_KEY` in `.env`.

	php artisan key:generate
	
```
APP_KEY=
```

`Elastic Beanstalk-> Create environment-> Create a web server environment`.

[(5:50)]( https://youtu.be/ISVaMijczKc?t=350 ) `Compress` all files in this folder to make `zip-archive`.

`Environment information`.

![screenshot of sample]( https://github.com/mslobodyanyuk/aws-laravel_academind/blob/main/public/images/aws/2.png ) 

`Platform`.

![screenshot of sample]( https://github.com/mslobodyanyuk/aws-laravel_academind/blob/main/public/images/aws/3.png ) 

[(6:20)]( https://youtu.be/ISVaMijczKc?t=380 ) `Upload` our code in `Elastic Beanstalk`.

`Application code`.

`Choose file`.

![screenshot of sample]( https://github.com/mslobodyanyuk/aws-laravel_academind/blob/main/public/images/aws/4.png ) 

[(7:40)]( https://youtu.be/ISVaMijczKc?t=460 ) 

`Create environment`.

[(7:55)]( https://youtu.be/ISVaMijczKc?t=475 ) 
_"We get a `Link` you can visit our `Application`. So let's `Click` it."_

`Forbidden`.

[(9:00)]( https://youtu.be/ISVaMijczKc?t=540 ) `Elastic Beanstalk-> Environments-> Environment_Name-> Configuration`. Change Configuration.

- Document root.

![screenshot of sample]( https://github.com/mslobodyanyuk/aws-laravel_academind/blob/main/public/images/aws/5.png )

`Apply`.

[(10:20)]( https://youtu.be/ISVaMijczKc?t=620 ) 
_"Visit Application again."_

[(10:30)]( https://youtu.be/ISVaMijczKc?t=630 ) `Register`. 

Error:

_"Connection refused"_

_"(2/2) QueryException"_

_"SQLSTATE[HY000] [2002] Connection refused (SQL: select count(*) as aggregate from `users` where `email` = maximus@gmail.com)"_

_"- Got No database here..."_

[(12:25)]( https://youtu.be/ISVaMijczKc?t=745 )
_"We can create a new RDS databse."_
`RDS( Relatonal Database Service )`. `Add database`.

`Elastic Beanstalk-> Environments-> Environment_Name-> Configuration-> Database-> Edit`. 
		
	root
	
	********
	
![screenshot of sample]( https://github.com/mslobodyanyuk/aws-laravel_academind/blob/main/public/images/aws/6.png )

![screenshot of sample]( https://github.com/mslobodyanyuk/aws-laravel_academind/blob/main/public/images/aws/7.png )

`Apply`.

[(14:35)]( https://youtu.be/ISVaMijczKc?t=875 ) `.env` 

_"- Would be nice if if there would be a more dynamic way of getting access to this values... Elastic Beanstalk it turns out it also gives you access to the database settings on the server superglobal."_

[(15:40)]( https://youtu.be/ISVaMijczKc?t=940 ) `config/database.php`:

```php
define('RDS_HOSTNAME', $_SERVER['RDS_HOSTNAME']);
define('RDS_USERNAME', $_SERVER['RDS_USERNAME']);
define('RDS_PASSWORD', $_SERVER['RDS_PASSWORD']);
define('RDS_DB_NAME', $_SERVER['RDS_DB_NAME']);
...
'mysql' => [
	'driver' => 'mysql',
	'host' => RDS_HOSTNAME,
	'port' => env('DB_PORT', '3306'),
	'database' => RDS_DB_NAME,
	'username' => RDS_USERNAME,
	'password' => RDS_PASSWORD,
...			
```

[(19:00)]( https://youtu.be/ISVaMijczKc?t=1140 ) `app/Providers/AppServiceProvider.php`:

```php
use Schema;
...
public function boot()
{
	Schema::defaultStringLength(191);
}
```

[(19:40)]( https://youtu.be/ISVaMijczKc?t=1180 ) `"migrations"`.

[(21:15)]( https://youtu.be/ISVaMijczKc?t=1275 ) 
_"Create folder `.ebextensions`."_

_"Create file with command `init.config`"_

```
container_commands: 
	01initdb:
		command: "php artisan migrate"
```

_"Replace `Tabs` with `Spaces`."_

[(24:00)]( https://youtu.be/ISVaMijczKc?t=1440 ) 
_"In our project folder `Delete` old archive. Then `Select` everything here and `Compress` again."_

[(24:20)]( https://youtu.be/ISVaMijczKc?t=1460 ) `Upload and Deploy`.

![screenshot of sample]( https://github.com/mslobodyanyuk/aws-laravel_academind/blob/main/public/images/aws/8.png )

[(25:00)]( https://youtu.be/ISVaMijczKc?t=1500 ) _"Let's Click this( Link ). And try registration again."_

_"Connection refused"_

[(25:25)]( https://youtu.be/ISVaMijczKc?t=1525 ) 
_"Failed to Deploy the Application."_

[(26:10)]( https://youtu.be/ISVaMijczKc?t=1570 ) _"This will remove this annoying folder:"_

	zip -d laravel-academind-blogv2.zip __MACOSX/\*

It works for me with these changes.
===================================

1. AWS - Platform: `PHP 7.4 running on 64bit Amazon Linux 2/3.3.7`

Configure more options->

Proxy Server: `Apache`

Document root: `/public`
									 
2. Update PHP version -> `php 7.4` in `composer.json`:

```js
"require": {
	"php": ">=7.4",		
```		

	`+`

	composer install
						
3. In `.env`:

```		  
...
APP_ENV=production
...
```

4. Error:

_"QueryException"_

_"SQLSTATE[42000]: Syntax error or access violation: 1231 Variable 'sql_mode' can't be set to the value of 'NO_AUTO_CREATE_USER' (SQL: select count(*) as aggregate from `users` where `email` = maximus@gmail.com)"_
						
<https://stackoverflow.com/questions/49949526/laravel-mysql-migrate-error> 

In `config/database.php`:

```php
...
'strict' => false,
...
```	
	
5. Error:

_"QueryException"_

_"SQLSTATE[42S02]: Base table or view not found: 1146 Table 'ebdb.users' doesn't exist (SQL: select count(*) as aggregate from `users` where `email` = maximus@gmail.com)"_

<https://stackoverflow.com/questions/30159257/base-table-or-view-not-found-1146-table-laravel-5>

Add in `app/User.php`:

```php
...
protected $table= "users";																													
...	
```	

6. 

<https://stackoverflow.com/questions/33640057/how-can-i-tell-if-elastic-beanstalk-is-running-my-config-files>

In `.ebextensions/init.config` use the `"--force"` flag.

```
container_commands: 
	01initdb:
		command: "php artisan migrate --force"
```			

---

[(26:30)]( https://youtu.be/ISVaMijczKc?t=1590 ) `Upload and Deploy again`.

![screenshot of sample]( https://github.com/mslobodyanyuk/aws-laravel_academind/blob/main/public/images/aws/9.png )

![screenshot of sample]( https://github.com/mslobodyanyuk/aws-laravel_academind/blob/main/public/images/aws/10.png )

[(27:00)]( https://youtu.be/ISVaMijczKc?t=1620 ) `Let's try this Registration process here again`.

![screenshot of sample]( https://github.com/mslobodyanyuk/aws-laravel_academind/blob/main/public/images/firefox/1.png )

![screenshot of sample]( https://github.com/mslobodyanyuk/aws-laravel_academind/blob/main/public/images/firefox/2.png )

[(27:15)]( https://youtu.be/ISVaMijczKc?t=1635 ) _"Now it seems successfuly Create a User. Enter the Post and see if that all the works and it does."_

![screenshot of sample]( https://github.com/mslobodyanyuk/aws-laravel_academind/blob/main/public/images/firefox/3.png )

#### Useful links:

Academind	

[Deploying a Laravel App via Elastic Beanstalk | Amazon Web Services BASICS]( https://www.youtube.com/watch?v=ISVaMijczKc&ab_channel=Academind )

<https://github.com/academind/laravel-simple-blog>

---

<https://stackoverflow.com/questions/33640057/how-can-i-tell-if-elastic-beanstalk-is-running-my-config-files>

---

Possible Errors

<https://stackoverflow.com/questions/49949526/laravel-mysql-migrate-error> 

<https://stackoverflow.com/questions/30159257/base-table-or-view-not-found-1146-table-laravel-5>