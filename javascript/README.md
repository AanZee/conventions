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

## Variables should be declared on a separate line

**Right:**
```javascript
let a = 1;
let b = 2;
let	c = 3;
let d = 4;
```
**Wrong:**
```javascript
let a = 1, b = 2, c = 3, d = 4;

let a = 1,
    b = 2,
    c = 3,
    d = 4;
```

## Write variables in camelCase
When const and let are available use camelCase for both.

**Right:**
```javascript
let willChange = 1;
const maxItems = 3;
```
**Wrong:**
```javascript
let will_change = 1;
const MAX_ITEMS = 3;
```

## Fat arrow functions
Use 'fat-arrow' functions when available.

**Right:**
```javascript
getItem().then((value: any) => {
	console.log(value);
});
```
**Wrong:**
```javascript
getItem().then(function(value: any) {
	console.log(value);
});
```

## Comments
Write comments that comply to the following format.

### Single line comments
```javascript
// Single line comment
```

### Multiline comments
```javascript
/**
 * Multiline comment
 * For comments too big for a single line
 */
```

### Method definition comments
```javascript
/**
 * Method description
 * @param  {} options [description]
 * @return {string} [description]
 */
```

### TODO comments
See a list of available tags in our '[Use special tags to mark comments](../general/README.md#use-special-tags-to-mark-comments)' section in the general conventions.

```javascript
// TODO: Single line comment
```