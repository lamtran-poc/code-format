## Table of contents

### Formatting
* [2 Spaces for indentation](#2-spaces-for-indentation)
* [Newlines](#newlines)
* [No trailing whitespace](#no-trailing-whitespace)
* [80 characters per line](#80-characters-per-line)
* [Use single quotes](#use-single-quotes)
* [Opening braces go on the same line](#opening-braces-go-on-the-same-line)
* [Declare one variable per var statement](#declare-one-variable-per-var-statement)

### Naming Conventions
* [Use lowerCamelCase for variables, properties and function names](#use-lowercamelcase-for-variables-properties-and-function-names)
* [Use UpperCamelCase for class names](#use-uppercamelcase-for-class-names)
* [Use UPPERCASE for Constants](#use-uppercase-for-constants)

### Variables
* [Declaration](#declaration)
* [Object / Array creation](#object--array-creation)

### Conditionals
* [Use the === operator](#use-the--operator)
* [Use descriptive conditions](#use-descriptive-conditions)

### Functions
* [Write small functions](#write-small-functions)
* [Return early from functions](#return-early-from-functions)
* [Return after a blank](#return-after-a-blank)
* [No nested closures](#no-nested-closures)
* [Method chaining](#method-chaining)

### Comments
* [Use slashes for comments](#use-slashes-for-comments)

### Miscellaneous
* [Object.freeze, Object.preventExtensions, Object.seal, with, eval](#objectfreeze-objectpreventextensions-objectseal-with-eval)
* [Requires At Top](#requires-at-top)
* [Getters and setters](#getters-and-setters)
* [Do not extend built-in prototypes](#do-not-extend-built-in-prototypes)

## Formatting

### 2 Spaces for indentation

Use 2 spaces for indenting your code and swear an oath to never mix tabs and
spaces - a special kind of hell is awaiting you otherwise.

### Newlines

Use UNIX-style newlines (`\n`), and a newline character as the last character
of a file. Windows-style newlines (`\r\n`) are forbidden inside any repository.

### No trailing whitespace

Just like you brush your teeth after every meal, you clean up any trailing
whitespace in your JS files before committing. Otherwise the rotten smell of
careless neglect will eventually drive away contributors and/or co-workers.

### 80 characters per line

Limit your lines to 80 characters. Yes, screens have gotten much bigger over the
last few years, but your brain has not. Use the additional room for split screen,
your editor supports that, right?

### Use single quotes

Use single quotes, unless you are writing JSON.

*Right:*

```js
const foo = 'bar';
```

*Wrong:*

```js
const foo = "bar";
```

### Opening braces go on the same line

Your opening braces go on the same line as the statement.

*Right:*

```js
if (true) {
  console.log('winning');
}
```

*Wrong:*

```js
if (true)
{
  console.log('losing');
}
```

Also, notice the use of whitespace before and after the condition statement.

### Declare one variable per var statement

Declare one variable per var statement, it makes it easier to re-order the
lines. However, ignore [Crockford][crockfordconvention] when it comes to
declaring variables deeper inside a function, just put the declarations wherever
they make sense.

*Right:*

```js

let values = [23, 42];
let keys = ['foo', 'bar'];
let object = {};

while (keys.length) {
  let key = keys.pop();
  object[key] = values.pop();
}
```

*Wrong:*

```js
let keys = ['foo', 'bar'],
    values = [23, 42],
    object = {},
    key;

while (keys.length) {
  key = keys.pop();
  object[key] = values.pop();
}
```

[crockfordconvention]: http://javascript.crockford.com/code.html

## Naming Conventions

### Use lowerCamelCase for variables, properties and function names

Variables, properties and function names should use `lowerCamelCase`.  They
should also be descriptive. Single character variables and uncommon
abbreviations should generally be avoided.

*Right:*

```js
const adminUser = db.query('SELECT * FROM users ...');
```

*Wrong:*

```js
const admin_user = db.query('SELECT * FROM users ...');
```

### Use UpperCamelCase for class names

Class names should be capitalized using `UpperCamelCase`.

*Right:*

```js
class BankAccount {
}
```

*Wrong:*

```js
function bank_Account() {
}
```

### Use UPPERCASE for Constants

Constants should be declared as regular variables or static class properties,
using all uppercase letters.

*Right:*

```js
const SECOND = 1 * 1000;

function myFile() {
}
myFile.FULL_PERMISSIONS = 0777;
```

*Wrong:*

```js
const SECOND = 1 * 1000;

function myFile() {
}
myFile.fullPermissions = 0777;
```

[const]: https://developer.mozilla.org/en/JavaScript/Reference/Statements/const

## Variables

### Declaration

Use *const* for immutable variable and *let* for mutable variables

*Right:*

```js
const a = ['hello', 'world'];
const b = {
  good: 'code',
  'is generally': 'pretty',
};

let c = {}
c.new = 1;

```

*Wrong:*

```js
const a = ['hello', 'world'];
a.push('!!!')

const b = {
  good: 'code',
  'is generally': 'pretty',
};
b.butNoThis = true;


let c = {}

```

### Object / Array creation

Use trailing commas and put *short* declarations on a single line. Only quote
keys when your interpreter complains:

*Right:*

```js
const a = ['hello', 'world'];
const b = {
  good: 'code',
  'is generally': 'pretty',
};
```

*Wrong:*

```js
const a = [
  'hello', 'world'
];
const b = {"good": 'code'
        , is generally: 'pretty'
        };
```

## Conditionals

### Use the === operator

Programming is not about remembering [stupid rules][comparisonoperators]. Use
the triple equality operator as it will work just as expected.

*Right:*

```js
const a = 0;
if (a !== '') {
  console.log('winning');
}

```

*Wrong:*

```js
const a = 0;
if (a == '') {
  console.log('losing');
}
```

[comparisonoperators]: https://developer.mozilla.org/en/JavaScript/Reference/Operators/Comparison_Operators

### Use descriptive conditions

Any non-trivial conditions should be assigned to a descriptively named variable or function:

*Right:*

```js
const isValidPassword = password.length >= 4 && /^(?=.*\d).{4,}$/.test(password);

if (isValidPassword) {
  console.log('winning');
}
```

*Wrong:*

```js
if (password.length >= 4 && /^(?=.*\d).{4,}$/.test(password)) {
  console.log('losing');
}
```

## Functions

### Write small functions

Keep your functions short. A good function fits on a slide that the people in
the last row of a big room can comfortably read. So don't count on them having
perfect vision and limit yourself to ~15 lines of code per function.

### Return early from functions

To avoid deep nesting of if-statements, always return a function's value as early
as possible.

*Right:*

```js
function isPercentage(val) {
  if (val < 0) {
    return false;
  }

  if (val > 100) {
    return false;
  }

  return true;
}
```

*Wrong:*

```js
function isPercentage(val) {
  if (val >= 0) {
    if (val < 100) {
      return true;
    } else {
      return false;
    }
  } else {
    return false;
  }
}
```

### Return after a blank

To help team member debug easier, put a blank before returning
when possible.

*Right:*

```js
function isPercentage(val) {
  if (val < 0) {
    return false;
  }

  return true;
}
```

*Wrong:*

```js
function isPercentage(val) {
  if (val < 0) {
    return false;
  }
  return true;
}
```

### No nested closures

Use closures, but don't nest them. Otherwise your code will become a mess.

*Right:*

```js
setTimeout(() => {
  client.connect(afterConnect);
}, 1000);

function afterConnect() {
  console.log('winning');
}
```

*Wrong:*

```js
setTimeout(() => {
  client.connect(function() {
    console.log('losing');
  });
}, 1000);
```


### Method chaining

One method per line should be used if you want to chain methods.

You should also indent these methods so it's easier to tell they are part of the same chain.

*Right:*

```js
User
  .findOne({ name: 'foo' })
  .populate('bar')
  .exec(function(err, user) {
    return true;
  });
```

*Wrong:*

```js
User
.findOne({ name: 'foo' })
.populate('bar')
.exec(function(err, user) {
  return true;
});

User.findOne({ name: 'foo' })
  .populate('bar')
  .exec(function(err, user) {
    return true;
  });

User.findOne({ name: 'foo' }).populate('bar')
.exec(function(err, user) {
  return true;
});

User.findOne({ name: 'foo' }).populate('bar')
  .exec(function(err, user) {
    return true;
  });
```

## Comments

### Use slashes for comments

Use slashes for both single line and multi line comments. Try to write
comments that explain higher level mechanisms or clarify difficult
segments of your code. Don't use comments to restate trivial things.

*Right:*

```js
// 'ID_SOMETHING=VALUE' -> ['ID_SOMETHING=VALUE', 'SOMETHING', 'VALUE']
const matches = item.match(/ID_([^\n]+)=([^\n]+)/));

// This function has a nasty side effect where a failure to increment a
// redis counter used for statistics will cause an exception. This needs
// to be fixed in a later iteration.
function loadUser(id, cb) {
  // ...
}

const isSessionValid = (session.expires < Date.now());
if (isSessionValid) {
  // ...
}
```

*Wrong:*

```js
// Execute a regex
const matches = item.match(/ID_([^\n]+)=([^\n]+)/);

// Usage: loadUser(5, function() { ... })
function loadUser(id, cb) {
  // ...
}

// Check if the session is valid
const isSessionValid = (session.expires < Date.now());
// If the session is valid
if (isSessionValid) {
  // ...
}
```

## Miscellaneous

### Object.freeze, Object.preventExtensions, Object.seal, with, eval

Crazy shit that you will probably never need. Stay away from it.

### Requires At Top

Always put requires at top of file to clearly illustrate a file's dependencies. Besides giving an overview for others at a quick glance of dependencies and possible memory impact, it allows one to determine if they need a package.json file should they choose to use the file elsewhere.

### Getters and setters

Do not use setters, they cause more problems for people who try to use your
software than they can solve.

Feel free to use getters that are free from [side effects][sideeffect], like
providing a length property for a collection class.

[sideeffect]: http://en.wikipedia.org/wiki/Side_effect_(computer_science)

### Do not extend built-in prototypes

Do not extend the prototype of native JavaScript objects. Your future self will
be forever grateful.

*Right:*

```js
const a = [];
if (!a.length) {
  console.log('winning');
}
```

*Wrong:*

```js
Array.prototype.empty = function() {
  return !this.length;
}

const a = [];
if (a.empty()) {
  console.log('losing');
}
```
