# Testing

## `describe`
The `describe` function is used to group related tests together, and allows scoping of other functions such as `beforeEach`

``` js
describe('Custom Module', () => {
  // Applies only to tests in this describe block
  beforeEach(() => {
    return initializeDatabase();
  });

  test('allows a-z', () => {
    expect(isValidEntry('diego')).toBe(true);
  });

  test('does not allow numbers', () => {
    expect(isValidEntry('Mart1n')).toBe(false);
  });
});
```

## `describe.only`
`describe.only` function specifies the ONLY `describe` block of tests that will be ran for a file/module. Usually used for debugging purposes.
``` js
describe.only('Custom Module 1', () => {
    // will be run
});

describe('Custom Module 2', () => {
    // will be skipped
});
```

## `before`

_TODO_

## `after`
_TODO_

## `beforeEach`
This method will be ran before each of the tests in the suite are ran. Usefull for resetting some global state that all tests depend on.

``` js
const globalDatabase = makeGlobalDatabase();

beforeEach(() => {
  // Clears the database and adds some testing data.
  return globalDatabase.clear().then(() => {
    return globalDatabase.insert({testData: 'foo'});
  });
});

test('can find things', () => {
  return globalDatabase.find('thing', {}, results => {
    expect(results.length).toBeGreaterThan(0);
  });
});

test('can insert a thing', () => {
  return globalDatabase.insert('thing', makeThing(), response => {
    expect(response.success).toBeTruthy();
  });
});
```

## `afterEach`
This method will be ran after each of the tests in the suite are ran. Usefull for cleaning up temporary state used in tests.

``` js
const globalDatabase = makeGlobalDatabase();

function cleanUpDatabase(db) {
  db.cleanUp();
}

afterEach(() => {
  cleanUpDatabase(globalDatabase);
});

test('can find things', () => {
  return globalDatabase.find('thing', {}, results => {
    expect(results.length).toBeGreaterThan(0);
  });
});

test('can insert a thing', () => {
  return globalDatabase.insert('thing', makeThing(), response => {
    expect(response.success).toBeTruthy();
  });
});
```