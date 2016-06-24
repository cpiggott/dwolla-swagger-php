dwolla-swagger-php
=========

The new Dwolla API V2 SDK, as generated by [this fork of swagger-codegen](https://github.com/mach-kernel/swagger-codegen). 

## Version

1.0.10

## Installation

`DwollaSwagger` is available on [Packagist](https://packagist.org/packages/dwolla/dwollaswagger), and can therefore be installed with [Composer](https://getcomposer.org/). 

```
composer require dwolla/dwollaswagger
composer install
```

To use, just `require` your composer `autoload.php` file.
```php
require('../path/to/vendor/autoload.php');
```

## Quickstart

`DwollaSwagger` makes it easy for developers to hit the ground running with our API. Before attempting the following, you should ideally create [an application key and secret](https://www.dwolla.com/applications).

### Configuring a client

To get started, all you need to set is the `access_token` and `host` values. 

```php
DwollaSwagger\Configuration::$access_token = 'a token';

# For UAT/Sandbox
$apiClient = new DwollaSwagger\ApiClient("https://api-uat.dwolla.com/");

# For production
$apiClient = new DwollaSwagger\ApiClient("https://api.dwolla.com");
```

### List 10 customers

Now that we've set up our client, we can use it to make requests to the API. Let's retrieve 10 customer records associated with the authorization token used. 

```php
DwollaSwagger\Configuration::$access_token = 'a token';
$apiClient = new DwollaSwagger\ApiClient("https://api-uat.dwolla.com/");

$customersApi = new DwollaSwagger\CustomersApi($apiClient);
$myCusties = $customersApi->_list(10);
```

### Creating a new customer

To create a customer, we can either provide an (associative) `array` with the expected values, or a `CreateCustomer` object. 

```php
$location = $customersApi->create([
    'firstName' => 'Jennifer',
    'lastName' => 'Smith',
    'email' => 'jsmith@gmail.com',
    'phone' => '7188675309'
]);
```

#### or 

```php
$jenny = new DwollaSwagger\CreateCustomer();
$jenny->firstName = 'Jennifer';
$jenny->lastName = 'Smith';
$jenny->email = 'jsmith@gmail.com';
$jenny->phone = '7188675309'

$location = $customersApi.create($jenny);
```

`$location` will contain a URL to your newly created resource (HTTP 201 / Location header).

## Modules

`DwollaSwagger` contains `API` modules which allow the user to make requests, as well as `models` which are [DAOs](https://en.wikipedia.org/wiki/Data_access_object) that the library uses to serialize responses. 

### API
Each API module is named in accordance to ([Dwolla's API Spec](http://docsv2.dwolla.com/) and encapsulates all of the documented functionality. 

* `AccountsApi`
* `BusinessclassificationsApi`
* `CustomersApi`
* `DocumentsApi`
* `EventsApi`
* `FundingsourcesApi`
* `RootApi`
* `TransfersApi`
* `WebhooksApi`
* `WebhooksubscriptionsApi`

----------

API objects take an `ApiClient` argument, which you created [here](##Configuring a client).

##### Example 
```php
$documentsApi = new DwollaSwagger\DocumentsApi($apiClient);
```

### Models

Each model represents the different kinds of requests and responses that can be made with the Dwolla API. 

* `AccountInfo`
* `Amount`
* `ApplicationEvent`
* `BaseObject`
* `BusinessClassification`
* `BusinessClassificationListResponse`
* `CreateCustomer`
* `CreateFundingSourceRequest`
* `CreateWebhook`
* `Customer`
* `CustomerListResponse`
* `Document`
* `DocumentListResponse`
* `EventListResponse`
* `FundingSource`
* `FundingSourceListResponse`
* `HalLink`
* `Money`
* `Transfer`
* `TransferListResponse`
* `TransferRequestBody`
* `Unit`
* `UpdateCustomer`
* `VerificationToken`
* `VerifyMicroDepositsRequest`
* `Webhook`
* `WebhookAttempt`
* `WebhookEventListResponse`
* `WebhookHeader`
* `WebhookHttpRequest`
* `WebhookHttpResponse`
* `WebhookListResponse`
* `WebhookRetry`
* `WebhookRetryRequestListResponse`
* `WebhookSubscription`

## Changelog

1.0.10
* Patch soft delete to deserialize with FundingSource model.

1.0.9
* Add boolean type to fix deserialization

1.0.8
* API schema updated, `FundingSourcesApi` supports balance check endpoint
* Fix transfer failure to support deserialization with new transfer failure model.

1.0.7
* API schema updated, `CustomersAPI` supports Customer search, new softDelete method in `FundingSourcesApi`. 

1.0.6
* API schema updated, `TransfersApi` has new endpoints for cancel a transfer and get a transfer's fees, new `OndemandauthorizationsApi`, new `MasspaymentsApi`. 
* Existing `Document`, `CreateFundingSourceRequest`, and `TransferRequestBody` models updated, new `MassPayment`, `Authorization`, `UpdateTransfer`, and `FacilitatorFeeRequest` models.

1.0.5
* API schema error fixed, `FundingSource` object now has `_embedded` key to fix serialization issues. 

1.0.4
* Avoid use of function names if found in list of PHP reserved words. 
* API schema updated, `CustomersApi` has new endpoints for IAV verification. 
* Existing `Customer` related models updated, new `VerificationToken` model.
* (release skipped, features in 1.0.5)

1.0.3
* API schema updated, `RootApi` now added.
* Changed `auth_token` to `access_token` in compliance with [RFC-6749](https://tools.ietf.org/html/rfc6749) recommended nomenclature.

1.0.2
* API schema updated, new methods in `FundingsourcesApi`.
* All methods which take Swagger variables in `path` (e.g, `/resource/{id}`) can now be passed a resource URL to make it easier for HAL-styled API consumption.
* More idiomatic response logic for HTTP 201 responses.

1.0.1
* API schema updated, new methods in `CustomersApi` and `TransfersApi`

1.0.0
* Initial release.

## Credits

This wrapper is semantically generated by a fork of [swagger-codegen](http://github.com/mach-kernel/swagger-codegen). 
 - [swagger-codegen contributors](https://github.com/swagger-api/swagger-codegen/network/members)
 - [David Stancu](http://github.com/mach-kernel)

## License

Copyright 2015 Swagger Contributors, David Stancu

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
