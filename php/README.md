# PHP

## PSR-2

Om de leesbaarheid van alle code te vergroten is het een goed idee om richting een standaard te gaan waar we ons allemaal aan confirmeren. De PHP wereld heeft hier een mooie standaard voor ontwikkeld: De PSR-2 standaard. Ik zal hier voor de meest gebruikte IDE's een link te posten naar hoe je deze standaard kunt instellen:

PHPStorm: https://confluence.jetbrains.com/display/PhpStorm/PHP+Code+Sniffer+in+PhpStorm

Sublime: @todo

## SOLID
Blijf zo veel mogelijk SOLID. Dit zorgt ervoor dat de code begrijpelijk en onderhoudbaar blijft, dus:

1. Niet alles bij elkaar in een class gooien en het vervolgens een 'helper' noemen.
2. Controllers zijn enkel bedoeld voor het afhandelen van input/output. En dus niet om diverse business logica in te gooien. Daar kun je bijvoorbeeld een service, repository (indien logica database gerelateerd, zoals een query) of desnoods een goed afgebakende helper voor gebruiken. 

Leesvoer: https://scotch.io/bar-talk/s-o-l-i-d-the-first-five-principles-of-object-oriented-design

## Testbaarheid
Indien er bijvoorbeeld links en rechts BookingHelpers worden geïnstantieerd is een dergelijke class/functie niet afzonderlijk te testen. Je krijgt gratis al het extra spul erbij wat in de geïnstantieerde class zit. Daarom ALLE dependencies injecteren via de desbetreffende class constructor (ook facades dus zo veel mogelijk vermijden). Indien je dit doet kun je tijdens het testen eenvoudig een dergelijke dependency 'wegmocken'.


Niet

```php
public function putArrivalAndDeparture(Request $oRequest)
{
    //...
    $oBookingHelper = new BookingHelper();
    //..
}
```

Wel

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
public function __construct(BookingHelper $bookingHelper){
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

Zie: https://jtreminio.com/2013/03/unit-testing-tutorial-part-4-mock-objects-stub-methods-dependency-injection/


## Algemene styling tips

**Doc block:**

Elke class, method/functie, constante en property horen een beschrijving te krijgen wat deze doet. Idealiter in de vorm van een doc block. Tevens worden deze doc blocks door IDE's gebruikt om de programmeur te helpen in de vorm van code completion.

```php
/**
 * Class UserFileReaderJob
 *
 * @package App\Jobs
 *
 * @author Kacper Kowalski kacper@aanzee.nl
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

Sinds PHP 7 type hinting (en return types) ondersteunt is het niet meer nodig om variabelen te prefixen met een data type. Deze kun je dus gewoon in camelcase specificeren. Bijvoorbeeld: $sQueryParam => $queryParam.

```php
/**
* Modify the rules for a given query param
*
* @param string $queryParam
* @param string $rules
*/
protected function updateQueryParamRules(string $queryParam, string $rules)
```