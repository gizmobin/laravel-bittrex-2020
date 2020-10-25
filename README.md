# Laravel-Bittrex

Start trading on Bittrex right away using your favorite PHP framework.

**Original work from pepijnolivier/laravel-bittrex**

Other contributors :  rpijpers, angelkurten

This is a roll-up of work to create a clean master (initially) for my own projects.

Including support for Laravel >=5.6

### Installation

`composer require gizmobin/laravel-bittrex`.

Add the service provider to your `config/app.php`:
 
```php
 'providers' => [
    gizmobin\Bittrex\BittrexServiceProvider::class,
 ],
 ```
 
...run `php artisan vendor:publish` to copy the config file.

Edit the `config/bittrex.php` or add Bittrex api and secret in your `.env` file

```
BITTREX_KEY={YOUR_API_KEY}
BITTREX_SECRET={YOUR_API_SECRET}
```

Add the alias to your `config/app.php`:

```php   
'aliases' => [
    'Bittrex' => gizmobin\Bittrex\Bittrex::class,
],
```

### Usage

Please refer to the [Api Documentation](https://bittrex.com/home/api) for more info, or read the [docblocks](https://github.com/gizmobin/laravel-bittrex/blob/master/src/Client.php) !

```php
use gizmobin\Bittrex\Bittrex;

// default is array, otherwise 'object' can be specified
Bittrex::getReturnType();
Bittrex::setReturnType($returnType);

// public API methods
Bittrex::getMarkets();
Bittrex::getCurrencies();
Bittrex::getTicker($market);
Bittrex::getMarketSummaries();
Bittrex::getMarketSummary($market);
Bittrex::getOrderBook($market, $type, $depth=20);
Bittrex::getMarketHistory($market);

// Public API 2.0 methods
Bittrex::getValidChartDataTickIntervals();
Bittrex::getChartData($market, $tickInterval='hour');

// market API methods
Bittrex::buyLimit($market, $quantity, $rate);
Bittrex::sellLimit($market, $quantity, $rate);
Bittrex::cancelOrder($uuid);
Bittrex::getOpenOrders($market=null);

// account API methods
Bittrex::getBalances();
Bittrex::getBalance($currency);
Bittrex::getDepositAddress($currency);
Bittrex::withdraw($currency, $quantity, $address, $paymentId=null);
Bittrex::getOrder($uuid);
Bittrex::getOrderHistory($market=null);
Bittrex::getWithdrawalHistory($currency=null);
Bittrex::getDepositHistory($currency=null);

// For multiple accounts
Bittrex::setAuthKey($key);
Bittrex::setAuthSecret($secret);	  
```
### Sample output based on use of returnType
<img src="/images/2020-10-25_14-01-42.jpg" border="1"/>

```php
	Bittrex::setReturnType('object');
	
	$data = Bittrex::getMarketSummaries();
	echo $data->result[0]->MarketName;
	var_dump($data->result[0]);
	dd($data);
```

```php
	Bittrex::setReturnType('array');   // default
	
	$data = Bittrex::getMarketSummaries();
	echo $data['result'][0]['MarketName'] . '<br/>';
	echo print_r($data['result'][0],true);
	dd($data);
```

This package is provided as-is. Do with it what you want ! PR's will be looked into.
I personally believe in freedom and equality, which is one of the reasons I'm in crypto.
It's also the reason I'm sharing most of the reusable code I write.
