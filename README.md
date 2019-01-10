# sparkpost-bundle [![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](https://github.com/Hanfrey/sparkpost-bundle/blob/master/LICENSE)

Bundle for using PeytzSend (Sparkpost) in symfony
Forked from https://github.com/Hanfrey/sparkpost-bundle

# Installation

## Step 1) Get the bundle 

    composer require peytz/peytzsend-bundle

## Step 2) Register the bundle

To start using the bundle, register it in your Kernel.

``` php
<?php
// app/AppKernel.php
public function registerBundles()
{
    $bundles = array(
        // ...
        new Peytz\PeytzsendBundle\PeytzsendBundle(),
        // ...
    );
}
```

## Step 3) Configure the default API token to use (mandatory)


Here is an example:
```yaml
# app/config/config.yml
peytz_peytzsend:
    api_token: 1212334ba # replace with your own
    api_host: api.eu.sparkpost.com
```

## Step 4) Example Usage in a controller

```php

$ps_client = $this->get("peytz_peytzsend.api_client");

try {
    // Build your email and send it!
    $results = $ps_client->transmission->send([
        'from'=>'From Envelope <from@example.com>',
        'html'=>'<html><body><h1>Congratulations, {{name}}!</h1><p>You just sent your very first mailing!</p></body></html>',
        'text'=>'Congratulations, {{name}}!! You just sent your very first mailing!',
        'substitutionData'=>['name'=>'YOUR FIRST NAME'],
        'subject'=>'First Mailing From PHP',
        'recipients'=>[
            [
                'address'=>[
                    'name'=>'YOUR FULL NAME',
                    'email'=>'YOUR EMAIL ADDRESS'
                ]
            ]
        ]
    ]);
    echo 'Woohoo! You just sent your first mailing!';
} catch (\Exception $err) {
    echo 'Whoops! Something went wrong';
    var_dump($err);
}
```

## Documentation

Detailed documentation on how to access each API method can be found in the documentation of the package that this bundle integrates: [Sparkpost API library](https://github.com/SparkPost/php-sparkpost/blob/master/README.md)
