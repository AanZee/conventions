# TypeScript

## Type definition
Wherever applicable, define variable types as specific as possible. Do this for all variables, parameters and return types.

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

### Exceptions

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

### Spacing
Type definitions are always preceded by a space (the semicolon connects to the method/variable).

**Right:**
```typescript
let a: string[] = ['a', 'b', 'c'];
```
**Wrong:**
```typescript
let a : string[] = ['a', 'b', 'c'];
let b:string[] = ['a', 'b', 'c'];
```

## Privates/Publics
Always define whether a class variable or method is private. Use private declarations only in your current file/scope. In some frameworks a private variable/method can be accessed by the template, however we decided to expose variables/methods as public to the template.

Don't define private/public for variables and methods that aren't properties of your class.

We don't know if we like to add the public keyword yet. Because everything in TypeScript (and JavaScript) is public by default:

**Right:**
```typescript
title: string = 'title';
private list: any[] = [];
private addItemToList(item: string): void {
	this.list.push(item);
};

public title: string = 'title';
private list: any[] = [];
private addItemToList(item: string): void {
	this.list.push(item);
};
```

**Wrong:**
```typescript
title: string = 'title';
list: any[] = [];
addItemToList(item: string): void {
	this.list.push(item);
};
```

## Comments
Define types in the comments
```typescript
/**
 * Method description
 * @param  {string} options [description]
 * @return {any[]}          [description]
 */
```

## Order
- Class variables are always declared at the top of the class above any class method.
- Private class variables are declared before public class variables
- Private and public class methods can be defined in order of usage (for example, a private method can be placed in between 2 public methods if it is only used by the above public method)

## Naming
- Just like in [javascript](README.md#write-variables-in-camelcase), variables of any type are written in lower camelCase.
- Classes, Interfaces and Enums are written in upper CamelCase (e.g. 'ProductInterface').
- Classes get a suffix for what type of class it is (e.g. 'AppModule', 'AccountService' or 'CartComponent').
- Interfaces get a 'Interface' suffix (e.g. 'ProductInterface')

## Example code
```typescript
export class SomeClass {
	private a: string = '';

	constructor() {}

	private getA(): string {
		return this.a;
	}

	setA(value: string) {
		this.a = value;
	}

	getTitle(): string {
		return this.getA();
	}
}
```
