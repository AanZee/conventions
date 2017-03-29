# JavaScript

## Framework specific
- [Angular 1 (by John Papa)](https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md)
- [Angular 2](angular-2.md)
- [jQuery](jquery.md)

## Quotes
Strings should be quoted with a single quote.

**Right:**
```javascript
let a = 'a';
```

**Wrong:**
```javascript
let a = "a";
```

## Target dom elements with a js- prefixed attribute

**Right:**
```javascript
document.querySelectorAll('[js-component]');
```

**Wrong:**
```javascript
document.querySelectorAll('.component');

document.querySelectorAll('[data-component]');

document.querySelectorAll('[component]');
```