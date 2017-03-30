# Unit testing

## Test driven development

### Write tests first, and let them fail
Always write your tests first. These will fail inevitable, since the code you are testing doesn't exist yet. Try to think of it as writing specs for your functionality first.

```js
const component = require('my-future-component.js');
describe('Components: My Future Component', () => {

	// will fail, since component.method() doesn't exist yet
	it('should do this and return that', () => {
		const parameter = 'Lorem ipsum dolor sit amet';
		expect(component.someMethod(parameter)).toBe(true);
	});

	// will fail too, for the same reason
	it('should do that and return this', () => {
		const condition = true;
		expect(component.anotherMethod(condition)).toEqual({
			property: 'value'
		});
	});

	it('should render this and that', () => {});

	it('should change that...', () => {});

	// Etc.
});
```

### Develop your code to let the tests pass
After writing your tests and seeing them fail, it's time to write your actual code. Let the tests run simultaneously to speed up development.

```js
const someMethod = parameter => {
	return parameter === 'Lorem ipsum dolor sit amet';
};
exports.method = method;

const anotherMethod = condition => {
	return condition
		? { property: 'value' }
		: { property: 'something else' };
};
exports.anotherMethod = anotherMethod;
```

The previously written tests should pass now. The benefits of this approach:

- You have tests guarding your codes **from the very start**
- You have **documentation for your code** from the start, helping other developers whom are new to the project
- You instantly see it if someone (that could be yourself in the long run) **breaks your code**

### Let tests run simultaneously. Always

All team members in a project should run the tests for the shared codebase simultaneously during development. The following example shows how to do this for a Node based project (in this case, an Angular 2 project):

```shell
# In one console tab/window
$ npm run test-watch

# In another
$ npm start
```