#REST

##Stateless

Tenzij we het hebben over een volledige applicatie houdt een API geen state bij. Zaken als bijvoorbeeld Redis ten behoeve van session storage dienen dus achterwege te blijven. Caching is in een aantal gevallen wel wenselijk. Bijvoorbeeld om per gebruiker id een lijst met autorisatie slugs* bij te houden. Hiermee voorkomen we dat we bij elke request opnieuw de database moeten raadplegen.

*Een slug is een string die dient als identifier, bijvoorbeeld 'users.view' en 'users.modify'.

##Altijd HTTPS

##Endpoint design

**Gebruik zo veel mogelijk zelfstandige naamwoorden in meervound** 

**De juiste HTTP method** 

**Query parameters voor specifiekere queries**

Niet:
```php
/v1/allProducts
/v1/productByName
/v1/productsByClient
```
Wel:
```php
GET /v1/products
```

```php
GET /v1/products/1?name=
```

```php
GET /v1/products?client=
```

Dit zorgt ervoor dat de API compact en overzichtelijk blijft maar ondertussen wel flexibel genoeg is om aan alle wensen te voldoen.

##Consistente statuscodes

Extra info: https://www.codetinkerer.com/2015/12/04/choosing-an-http-status-code.html

##Responses

Idealiter retourneren we altijd JSON met daarin meta data welke extra informatie geeft over de specifieke aanroep. In zijn geheel ziet een succesvolle response er bijvoorbeeld zo uit:

```php
{
   "status": 200,
   "href": "https://api.domain.com/v1/products/",
   "meta": {
      "IP": "127.0.0.1",
      "method": "GET"
   },
   "products": [
      {
         "id": "4321",
         "href": "https://api.domain.com/v1/products/4321",
         "title": "product A"
      },
      {
         "id": "1234",
         "href": "https://api.domain.com/v1/products/1234",
         "title": "product B"
      }
   ]
}
```

In het geval van een fout willen we zo duidelijk mogelijk zijn:



```php
{
   "status": 400,
   "message": "There was a validation error. The input 'email' was invalid. Please see the documentation '/v1/documentation' for details about validation rules for this endpoint."
}
```

