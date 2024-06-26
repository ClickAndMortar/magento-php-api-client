# Magento / Adobe Commerce PHP API client

This is a PHP client for the Magento / Adobe Commerce REST API.

## Requirements

* PHP 8.2 or higher
* Magento / Adobe Commerce 2.3 or higher

## Installation

```bash
composer require clickandmortar/magento-api-client
```

## Usage

```php
<?php

require 'vendor/autoload.php';

use ClickAndMortar\MagentoApiClient\ClientBuilder;
use ClickAndMortar\MagentoApiClient\SearchCriteria\SearchCriteriaBuilder;

$clientBuilder = new ClientBuilder('https://magento.hostname.com/');
$client = $clientBuilder->buildAuthenticatedByOauth(
    '<consumer-key>>',
    '<consumer-secret>',
    '<access-token>',
    '<access-token-secret>'
);

// Fetch all products
$searchCriteriaBuilder = new SearchCriteriaBuilder();
$searchCriteriaBuilder->addFilter('type_id', 'simple');
$searchCriteriaBuilder->setPageSize(10);

foreach ($client->products->all($searchCriteriaBuilder->create()) as $product) {
    echo $product->sku . ' - ' . $product->name . PHP_EOL;
}

// Fetch a single product
$product = $client->products->get('24-MB01');
```

## Available resources

- `products`
- `orders`
- `customers`

## Credits

This library is heavily inspired by - and uses parts of - the [Akeneo PHP Client](https://github.com/akeneo/api-php-client), thanks for their amazing work 🧡.

## License

This project is licensed under the Open Software License version 3.0 - see the [LICENSE](LICENSE) file for details.

This project is not affiliated with, endorsed by, or sponsored by Adobe Inc.
"Magento" and "Adobe Commerce" are trademarks of Adobe Inc.
All trademarks and registered trademarks are the property of their respective owners.
