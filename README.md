# logviewer
Quick and dirty standalone PHP script for easy access to log files created by our proyects.

![Screenshot](https://github.com/nahun-accesium/logviewer/blob/master/screenshot.png)

##Features

* Single file, no dependencies
* Configure your log files using an array and regular expressions
* Responsive layout using Bootstrap
* Autorefresh log file (new lines are notified using browser notifications)
* See raw log file
* Download log file
* Remove files or zip and store
* Settings stored using browser's localStorage if available

##Settings

```php
// Sample settings
$settings = array(
	'apache' => array(
			'name' => 'Apache logs',
			'path' => 'system/logs/',
			'regexp' => '/apache-error.*?\.php/',
			'delimiter' => '/[\r\n]+/',
			'data_regexp' => '/^\[(.*?)\] \[(.*?)\] (.*)/sm',
			'data_keys' => array(
				'level' => 1,
				'date' => 0,
				'message' => 2,
				'dateformat' => 'D M d H:i:s.u Y' //[Fri Oct 23 10:00:53.404979 2015]
			)
		)
);
```

* `name` is used in the file selection menu
* `path` where the files are stored at
* `regexp` must be matched by the file names to be considered log files for this index
* `delimiter` is used to split the log in messages. In this case, the apache logfiles are single line messages, but you may have other projects where that's not the case. Check `codeigniter` sample for an example on how to split multi line log messages.
* `data_regexp` is a regexp used to capture the data from the message. Use capturing groups.
* `data_keys` matches the capturing groups with their meaning: `level`, `date` and `message`. The `dateformat` field is used to create a DateTime object with its "from-format" feature. If it fails, the DateTime will be created with a 'now' value.

#Disclaimer

This script was created to meet an internal need and its features are strongly binded to what we need from it at any given moment in time. Feel free to fork it but don't expect any support from our side.