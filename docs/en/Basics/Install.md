# Installation

## Composer Install

### Install SilverStripe and SwipeStripe

:::
	composer create-project --no-dev silverstripe/installer ./some-directory 3.1.0
	composer require swipestripe/swipestripe:2.1.*@dev
	php framework/cli-script.php dev/build flush=1

### Install payment module

:::
	composer require frankmullenger/payment-cheque:dev-master

#### Configure payment module

Update mysite/_config/config.yml by adding:

:::yaml
	---
	Name: payment
	After: 'framework/*','cms/*'
	---
	PaymentGateway:
	  environment:
	    'dev'
	PaymentProcessor:
	  supported_methods:
	    dev:
	      - 'Cheque'
	    live:
	      - 'Cheque'

:::
	php framework/cli-script.php dev/build flush=1

### Set base currency
After installing SwipeStripe it is a good idea to set a base currency - before you add products or process any orders.

Go to the Shop section and click on the "Settings" tab.  
Find the box for "Base Currency" and click "Edit base currency".  
Set the base currency, a [3 letter currency code](http://en.wikipedia.org/wiki/ISO_4217#Active_codes) and the symbol you want to use when displaying this currency.

### Install other SwipeStripe modules

:::
	composer require swipestripe/swipestripe-addresses:2.1.*@dev
	composer require swipestripe/swipestripe-category:2.1.*@dev
	composer require swipestripe/swipestripe-flatfeeshipping:2.1.*@dev
	composer require swipestripe/swipestripe-flatfeetax:2.1.*@dev
	composer require swipestripe/swipestripe-currency:2.1.*@dev
	composer require swipestripe/swipestripe-docs:2.1.*@dev

[List of SwipeStripe modules here](http://addons.silverstripe.org/add-ons/swipestripe)

## Manual Install

### Install SilverStripe
First install SilverStripe 3.1.*.

[How to install SilverStripe](http://doc.silverstripe.org/framework/en/installation/)

Log in to the admin area after you have installed SilverStripe.

### Install SwipeStripe
Once SilverStripe is installed you can install the SwipeStripe and SilverStripe Payment modules.

SwipeStripe is free to try, but *you MUST purchase a licence before deploying SwipeStripe to a live webserver*.

[Download the SwipeStripe module](https://github.com/frankmullenger/silverstripe-swipestripe)  
[Download the Payment module](https://github.com/silverstripe-labs/silverstripe-payment/tree/1.0)

Once you have downloaded the modules, unzip them and call the folders "swipestripe" and "payment" respectively.

Drop the folders into the root of your SilverStripe installation (alongside cms/ and framework/ folders) then run a build by appending /dev/build?flush=1 to the site's domain. 

e.g:  
If you installed SilverStripe at: http://swipestripe-test.local  
To run a build on this domain visit: http://swipestripe-test.local/dev/build?flush=1

#### Set base currency
After installing SwipeStripe it is a good idea to set a base currency - before you add products or process any orders.

Go to the Shop section and click on the "Settings" tab.  
Find the box for "Base Currency" and click "Edit base currency".  
Set the base currency, a [3 letter currency code](http://en.wikipedia.org/wiki/ISO_4217#Active_codes) and the symbol you want to use when displaying this currency.  

### Install Cheque Payment Module
In order to process test orders you will need to install a method of payment, the easiest payment method to start with (and for testing) is Cheque payment. 

In future you will likely install another payment method such as PaymentExpress, Paystation or PayPal to process credit card payments.

[Download the Cheque Payment module](http://swipestripe.com/assets/Uploads/Downloads/silverstripe-payment-cheque.zip)

Rename the folder "payment-cheque", drop it into the root folder of your SilverStripe install and run a build on your site again.

#### Configure Cheque Payment
After installing the cheque payment module you will need to enable it. In SilverStripe 3 configuration is achieved via YAML files. 

Create the file:  
/mysite/_config/Mysite.yaml

:::yaml
	Name: Mysite
	---
	 
	PaymentGateway:
	  environment:
	    'dev'
	 
	PaymentProcessor:
	  supported_methods:
	    dev:
	      - 'Cheque'
	    live:
	      - 'Cheque'

Run a /dev/build?flush=1 and the Cheque payment option should be available on your checkout page.

## Testing
Once you have installed the SwipeStripe and payment modules set your environment to "dev" for your testing. 

You can set environment in your _ss_environment.php

:::php
	/* What kind of environment is this: development, test, or live (ie, production)? */
	define('SS_ENVIRONMENT_TYPE', 'dev');

Or _config.php

:::php
	//Set dev environment
	Director::set_environment_type('dev');

The advantage of setting your site to dev mode while testing is that you can run a task to delete all test orders to clean up after you are finished testing in /dev/tasks.

You can also delete customers that do not have any orders from the CMS if you want to delete your testing customer account after that.
