# PHP

## PSR-2

To increase the readability of all the code, it is a good idea to go towards a standard that we all conform to. The PHP world has developed a nice standard for this: [The PSR-2 standard](https://www.php-fig.org/psr/psr-2). For the most used IDEs I will post a link here for how to set this up:

[PHPStorm code sniffer](https://confluence.jetbrains.com/display/PhpStorm/PHP+Code+Sniffer+in+PhpStorm)

Sublime: @todo

## SOLID

Stay as much SOLID as possible. This ensures that the code remains understandable and maintainable, so:

1. Do not throw everything together in a class and then call it a 'helper'.
2. Controllers are only intended for handling input / output. And not to throw in various business logic. You can, for example, use a service, repository (if code is database related, such as a query) or, if necessary, a well-defined helper.

A good read: https://scotch.io/bar-talk/s-o-l-i-d-the-first-five-principles-of-object-oriented-design

## Testability

If, for example, BookingHelpers are instantiated on several places, such a class / function can not be tested separately. Every attempt will result in automatically testing the instantiated class. Therefore, inject ALL dependencies via the relevant class constructor (so avoid facades as much as possible). This way, when you start testing you can just inject mocked classes instead of the actual stuff.


Right
```php
/**
*
* @var BookingHelper $bookingHelper 
*/
private $bookingHelper;

/**
* Constructor
*
* @param BookingHelper $bookingHelper
*
*/
public function __construct(BookingHelper $bookingHelper)
{
    $this->bookingHelper = $bookingHelper;
}

/**
* Set the arrival and departure of a booking
*
* @param Request $request Pass the request
*
*/
public function putArrivalAndDeparture(Request $request)
{
    //...
    $bookingHelper = $this->bookingHelper;
    //..
}
```
Wrong
```php
public function putArrivalAndDeparture(Request $oRequest)
{
    //...
    $oBookingHelper = new BookingHelper();
    //..
}
```


More info: https://jtreminio.com/2013/03/unit-testing-tutorial-part-4-mock-objects-stub-methods-dependency-injection/


## General advice

**Doc block:**

Every class, method / function, constant and property should have a description of what it does. Ideally in the form of a doc block. These doc blocks are also used by IDEs to help the programmer with code completion.

```php
/**
 * Class UserFileReaderJob
 *
 * @package App\Jobs
 *
 */
class UserFileReaderJob extends Job implements ShouldQueue
{
}
```

```php
/**
* Execute job
*
* @param ImportHelper $importHelper
*
* @throws Exception
*/
public function handle(ImportHelper $importHelper)
{
}
```

```php
/**
* Parameter name for requesting an expand
*/
const EXPAND = 'expand';

/**
 * Parameter name for requesting a limit
 */
const LIMIT = 'limit';

/**
 * Parameter name for requesting an offset
 */
const OFFSET = 'offset';
```

```php
/**
* @var Closure $callback The function to execute when we have a full document
*/
private $callback;
```

**Type hinting:**

Since PHP 7 supports type hinting (and return types) it is no longer necessary to prefix variables with a data type. You can therefore simply specify these in camelcase. For example: $sQueryParam => $queryParam.

```php
/**
* Modify the rules for a given query param
*
* @param string $queryParam
* @param string $rules
*/
protected function updateQueryParamRules(string $queryParam, string $rules)
```