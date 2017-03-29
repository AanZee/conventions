# JavaScript conventions

## Variables should be declared on a separate line.

**Right:**
```
var one = 1,
	two = 1,
	three = 1;
var four = 4;
```
**Wrong:**
```
var one = 1, two = 2,
three = 3;
var four = 4;
```

## Naming

### What does it do/represent?
Use names that explain the functionality or dataFormat.

**Right:**
```
private _itemList: any[] = [];

public getItemList(): any[] {
	return this.itemList;
}
```
**Wrong:**
```
let someName: any[] = [];

public doSomething(): any[] {
	return this.itemList;
}
```

## Comments
Write comments that comply to the following format.

### Single line comments
```
// Single line comment
```

### Multiline comments
```
/**
 * Multiline comment
 * For comments too big for a single line
 */
```

### Method definition comments
```
/**
 * Method description
 * @param  {} options [description]
 * @return {string} [description]
 */
```

### TODO comments
```
// TODO: Single line comment
```
