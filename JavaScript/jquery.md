# jQuery conventions

## Prefix jQuery objects with dollar sign
Prefix jQuery objects with dollar sign to recognize them in your code

**Right:**
```javascript
let $component = $('.component');

$component.addClass('is-hidden');
```

**Wrong:**
```javascript
let component = $('.component');

component.addClass('is-hidden');
```