# TypeScript

## Type definition
Type definitions are always preceded by a space (the semicolon connects to the method/variable).
**Right:**
```typescript
let a: string[] = ['a','b','c'];
```
**Wrong:**
```typescript
let a : string[] = ['a','b','c'];
```

## Privates/Publics
Always define whether a class variable or method is private or public. In Angular2 a private variable/method can be accessed by the template.

Don't do this for variables and methods that are not properties of your class.

**Right:**
```typescript
private list: any[] = [];
public addItemToList(value: any): void {
	let item: any = value;
	this.list.push(item);
};
```
**Wrong:**
```typescript
list: any[] = [];
addItemToList(value: any): void {
	let item: any = value;
	this.list.push(item);
};
```

## Types
Wherever applicable, define variable types as specific as possible.
Do this for all variables, parameters and return types.

**Right:**
```typescript
public getItem(index: number): any {
	let item: any = itemList[index];
	return item;
};
```
**Wrong:**
```typescript
public getItem(index) {
	let item = itemList[index];
	return item;
};
```

Exceptions:

A constructor doesn't have to return a type.
```typescript
constructor() {}
```

Type definition is not possible in a `for in` loop.
```typescript
for (let key in object) {
}
```

Type definition is not possible for the return value in a `setter` method.
```typescript
public set message(value: string) {
	this._message = value;
}
```

### Comments
Define types in the comments
```typescript
/**
 * Method description
 * @param  {string} options [description]
 * @return {any[]}          [description]
 */
```

## Naming
### Private class variables
Private class variables always start with an underscore.

## Order
Class variables are always declared at the top of the class above any class method.

Private class variables are declared before public class variables

Private and public class methods can be defined in order of usage (for example, a private method can be placed in between 2 public methods if it is only used by the above public method)


## Example code
```typescript
import { Injectable } from '@angular/core';

@Injectable()
export class GAProvider {
	private _blah: string = '';

	public blah: string = '';
	public get blah(): string {
		return this._blah;
	}
	public set blah(value: string) {

	}

	// Lifecycle methods are defined above other methods
	constructor() {}

	ionViewWillEnter(): void {}

	public getSelectionArrayFromObject(object: any): any[] {
		let objectArray: any[] = [];

		for (let key in object) {
			if (object.hasOwnProperty(key)) {
				if (object[key] && object[key].active) {
					objectArray.push(object[key]);
				} else {
					console.log('Object is not active.', object[key]);
				}
			}
		}
	}

	private calculateThings(value1: number, value2: number): number {
		return value1 * value2;
	}
}
```
