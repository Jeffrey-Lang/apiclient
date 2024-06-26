[![Latest Stable Version](http://poser.pugx.org/planningsagenda/apiclient/v)](https://packagist.org/packages/planningsagenda/apiclient) [![Total Downloads](http://poser.pugx.org/planningsagenda/apiclient/downloads)](https://packagist.org/packages/planningsagenda/apiclient) [![Latest Unstable Version](http://poser.pugx.org/planningsagenda/apiclient/v/unstable)](https://packagist.org/packages/planningsagenda/apiclient) [![License](http://poser.pugx.org/planningsagenda/apiclient/license)](https://packagist.org/packages/planningsagenda/apiclient) [![PHP Version Require](http://poser.pugx.org/planningsagenda/apiclient/require/php)](https://packagist.org/packages/planningsagenda/apiclient)

# Google APIs Client Library for PHP #

## Description ##
The Google API Client Library enables you to work with Google APIs such as Google+, Drive, or YouTube on your server.

## Beta ##
This library is in Beta. We're comfortable enough with the stability and features of the library that we want you to build real production applications on it. We will make an effort to support the public and protected surface of the library and maintain backwards compatibility in the future. While we are still in Beta, we reserve the right to make incompatible changes. If we do remove some functionality (typically because better functionality exists or if the feature proved infeasible), our intention is to deprecate and provide ample time for developers to update their code.

## Requirements ##
* [PHP 5.2.1 or higher](http://www.php.net/)
* [PHP JSON extension](http://php.net/manual/en/book.json.php)

*Note*: some features (service accounts and id token verification) require PHP 5.3.0 and above due to cryptographic algorithm requirements. 

## Developer Documentation ##
http://developers.google.com/api-client-library/php

## Installation ##

For the latest installation and setup instructions, see [the documentation](https://developers.google.com/api-client-library/php/start/installation).

## Basic Example ##
See the examples/ directory for examples of the key client features.
```PHP
<?php

  require_once 'google-api-php-client/src/Google/autoload.php'; // or wherever autoload.php is located
  
  $client = new Google_Client();
  $client->setApplicationName("Client_Library_Examples");
  $client->setDeveloperKey("YOUR_APP_KEY");
  
  $service = new Google_Service_Books($client);
  $optParams = array('filter' => 'free-ebooks');
  $results = $service->volumes->listVolumes('Henry David Thoreau', $optParams);

  foreach ($results as $item) {
    echo $item['volumeInfo']['title'], "<br /> \n";
  }
  
```

### Service Specific Examples ###

YouTube: https://github.com/youtube/api-samples/tree/master/php

## Frequently Asked Questions ##

### What do I do if something isn't working? ###

For support with the library the best place to ask is via the  google-api-php-client tag on StackOverflow: http://stackoverflow.com/questions/tagged/google-api-php-client

If there is a specific bug with the library, please file a issue in the Github issues tracker, including a (minimal) example of the failing code and any specific errors retrieved. Feature requests can also be filed, as long as they are core library requests, and not-API specific: for those, refer to the documentation for the individual APIs for the best place to file requests. Please try to provide a clear statement of the problem that the feature would address.

### How do I contribute? ###

We accept contributions via Github Pull Requests, but all contributors need to be covered by the standard Google Contributor License Agreement. You can find links, and more instructions, in the documentation: https://developers.google.com/api-client-library/php/contribute

### I want an example of X! ### 

If X is a feature of the library, file away! If X is an example of using a specific service, the best place to go is to the teams for those specific APIs - our preference is to link to their examples rather than add them to the library, as they can then pin to specific versions of the library. If you have any examples for other APIs, let us know and we will happily add a link to the README above!

### Why do you still support 5.2? ###

When we started working on the 1.0.0 branch we knew there were several fundamental issues to fix with the 0.6 releases of the library. At that time we looked at the usage of the library, and other related projects, and determined that there was still a large and active base of PHP 5.2 installs. You can see this in statistics such as the PHP versions chart in the WordPress stats: http://wordpress.org/about/stats/. We will keep looking at the types of usage we see, and try to take advantage of newer PHP features where possible.

### Why does Google_..._Service have weird names? ###

The _Service classes are generally automatically generated from the API discovery documents: https://developers.google.com/discovery/. Sometimes new features are added to APIs with unusual names, which can cause some unexpected or non-standard style naming in the PHP classes. 

### How do I deal with non-JSON response types? ###

Some services return XML or similar by default, rather than JSON, which is what the library supports. You can request a JSON response by adding an 'alt' argument to optional params that is normally the last argument to a method call:

```
$opt_params = array(
  'alt' => "json"
);
```

### How do I set a field to null? ###

The library strips out nulls from the objects sent to the Google APIs as its the default value of all of the uninitialised properties. To work around this, set the field you want to null to Google_Model::NULL_VALUE. This is a placeholder that will be replaced with a true null when sent over the wire.

## Code Quality ##

Run the PHPUnit tests with PHPUnit. You can configure an API key and token in BaseTest.php to run all calls, but this will require some setup on the Google Developer Console.

    phpunit tests/

### Coding Style

To check for coding style violations, run

```
vendor/bin/phpcs src --standard=style/ruleset.xml -np 
```

To automatically fix (fixable) coding style violations, run  

```
vendor/bin/phpcbf src --standard=style/ruleset.xml
```
