# Unit testing

## Test driven development

### Why write unit tests?
Good tests are the best way to prevent errors from ending up in the final product. In that sense, they are more important than linting and static analysis which only check for errors on the surface (typos, style errors etc.), not the actual logic of your code.

In a nutshell, why bother testing?

- **Design better code**: writing tests first gives you a clearer idea of the API and help you achieve its most ideal design. When something is hard to test afterwards, you might have to reconsider your code.
- **Documentation for team members**: the feature descriptions of your tests help guide (new) developers through the code.
- **Automated quality assurance**: it's nearly impossible to remember all features of your code and how they act together. Good tests safeguard your code, making sure everything keeps working as intended.
- **Continuous delivery assurance**: by writing good tests from the start, you automatically prevent broken builds from being deployed to production.

### Write tests first, and let them fail
Always write your tests first. These will fail inevitable, since the code you are testing doesn't exist yet. Try to think of it as writing specs for your features first. Always ask yourself these two questions beforehand:

1. **What part/component of our codebase do I want to test?** (e.g. testing the return value of a certain feature method)
2. **What should my feature do?** (e.g. 'When we provide a certain parameter to someMethod() it should always return that same value')

Consider the following example:

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

These will fail inevitably for said reasons.

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

- You now have tests guarding this code **from the very start**, wich clears up your mind from having to remember how it works
- You now have **documentation for your feature** from the start, helping other developers whom are new to the project
- You instantly see it if someone (that could be yourself in the long run) **breaks your code**
- More importantly: this will keep working, and won't cause a build to break or worse: end up in production

### Let tests run simultaneously. Always

All team members in a project should run the tests for the shared codebase simultaneously during development. The following example shows how to do this for a Node based project (in this case, an Angular 2 project):

```shell
# In one console tab/window
$ npm run test-watch

# In another
$ npm start
```