Store special setting, config to database. No replace normal laravel config usage, only alternative for site settings.

## config/app.php additions ##

### Provider ###
Need to add to the beginning/top, otherwise you may receive an error when you use the any config file.

```php
'Juy\Setting\SettingServiceProvider'
```

### Alias ###

```php
'Setting' => 'Juy\Setting\Facades\Setting'
```

## Usage ##

```php
// Get single value
Setting::get('mail_driver');

// Set single value
Setting::set('mail_driver');

// Set multiple key, value
Setting::insert(array($key => $value));

// Set key, value from form post data
$post = Input::except('_token'); // except for token
Setting::insert($post);
```

## Migration ##

```shell
php artisan migrate --package=juy/setting
```

## Seed ##
There is no seed file, create one as you want.

```php
<?php

use Juy\Setting\Model\Setting;

class SettingsTableSeeder extends \Seeder {

	public function run()
	{
		DB::table('settings')->truncate();

		Setting::insert(array(
			// Mail
			array(
				'key'	=> 'mail_driver',
				'value'	=> 'smtp'
			),
			array(
				'key'	=> 'mail_host',
				'value'	=> 'smtp.mailgun.org'
			),
			array(
				'key'	=> 'mail_port',
				'value'	=> '587'
			),
			array(
				'key'	=> 'mail_encrypt',
				'value'	=> 'tls'
			),
			array(
				'key'	=> 'mail_smtpUser',
				'value'	=> ''
			),
			array(
				'key'	=> 'mail_smtpPass',
				'value'	=> ''
			)
		));

	}
}
```