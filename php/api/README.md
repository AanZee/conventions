# REST

## Stateless

Unless we are talking about a complete application, an API does not have a state. Caching for the benefit of session storage should be left out. Caching is desirable in a number of cases. For example, to keep a list of authorization slugs* per user. This prevents us from having to query the database on each request.

*A slug is essentially just a string that serves as an identifier, for example 'users.view' and 'users.modify'.

## Always use HTTPS

## Endpoint design

**Never use verbs and always use plural nouns** 

**The right HTTP method** 

**Use query parameters for more specific queries**

This ensures that the API remains compact and well-organized, but at the same time is flexible enough to meet all requirements.


**Right**
```php
GET /v1/products
GET /v1/products/1?name=
GET /v1/products?client=
```
**Wrong**
```php
/v1/allProducts
/v1/productByName
/v1/productsByClient
```

## Consistent status codes

More info: https://www.codetinkerer.com/2015/12/04/choosing-an-http-status-code.html

## Responses

Ideally, we always return pretty JSON with meta data that gives extra information about the specific call. In general, a successful response looks something like this:

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

## Error responses

In case of an error, we want to be as clear as possible:

```php
{
   "status": 400,
   "message": "There was a validation error. The input 'email' was invalid. Please see the documentation '/v1/documentation' for details about validation rules for this endpoint."
}
```

