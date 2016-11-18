# Jest Cheat Sheet

## Test structure

### Basic tests
```js
test('something', () => expect(something).toBe(true));
test('something else'< () => expect(somethingElse).toBe(true));

// use describe to group tests together.
// NOTE: Don't use `describe` if you have only one top level group.
describe('group tests together', () => {
  // use `test` to describe things
  test('something', () => expect(something).toBe(true));

  // use `it` to describe actions
  it('does something', () => expect(something).toBe(true));
});
```

### before/after hooks

```js
beforeEach(function() {
  // `this` is shared between all tests and their hooks, and gets reset automatically after a test is finished executing
  this.state = longComplicatedSetup();
});

test('one', function() {
  doSomething(this.state); // `this.state` is recreated for each test
  expect(this.state).toEqual(something);
});

test('two', function() {
  doSomething(this.state);
  expect(this.state).toEqual(something);
});
```

### skipping/focusing

```js
test.only('will run only this test');

test.skip('this test will be skipped');

describe.only('will run only tests inside this block', () => {
  // ...
});
```


## Matchers

[http://facebook.github.io/jest/docs/api.html#writing-assertions-with-expect](Documentation)

### .toBe(value)
```js
// will pass
expect(1).toBe(1);
expect('a').toBe('a');
// will fail
expect({a: 1}).toBe({a: 1});
expect(1).not.toBe(1);
```

### .toEqual(value);
```js
// will pass
expect({a: 1}).toEqual({a: 1});
expect(1).toEqual(1);
// will fail
expect({a: 1}).toEqual({a: 2});
```


### .toBeInstanceOf(Class)
```js
class A {}
// will pass
expect(new A).toBeInstanceOf(A);
// will fail
expect('aaa').toBeInstanceOf(Number);
```

### .toContain(item) .toContainEqual(item)
```js
// will pass
expect([1, 2, 3]).toContain(3);
expect([{a: 1}, {a: 2}]).toContainEqual({a: 1});
// will fail
expect([{a: 1}, {a: 2}]).toContain({a: 1});

```

### .toThrowError()
```js
// will pass
expect(() => { throw new Error('lol') }).toThrowError(/lol/);
```

### .toMatchSnapshot()
```js
// Works on everything that can be serialized.
// If different value is passed in the next run, the matcher will fail.
expect([1, 2, 3]).toMatchSnapshot();
```

### .toThrowErrorMatchingSnapshot()
```js
// Will create a snapshot containing error class and message
expect(() => { throw new Error('lol') }).toThrowErrorMatchingSnapshot();
```

## Other matchers
```
.toBeFalsy()
.toBeGreaterThan(number)
.toBeGreaterThanOrEqual(number)
.toBeLessThan(number)
.toBeLessThanOrEqual(number)
.toBeNull()
.toBeTruthy()
.toEqual(value)
.toMatch(regexp)
```
