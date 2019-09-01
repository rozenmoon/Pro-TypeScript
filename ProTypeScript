## Chapter 1
JS -> Javascript
TS -> Typescript

### All Javascript is valid TypeScript
-> If you transfer code form Javascript to .ts file it will be still fine (with few warning be me errors as well).
-> Common problem comes from dynamic type system in JS, different types can be assigned to a variable during its lifetime in JS.
-> TS compiler will generate sensible js code even when you receive errors or warning
-> Exception to "all js valid as ts rule" are "with" statement

```
// Not using with
var radius = 4;
var area = Math.PI * radius * radius;

// Using with
var radius = 4;
with (Math) {
    var area = PI * radius * radius;
}
```

-> 'with' is not allowed in strict mode of ES5 and ES6
-> ts will treat all statement inside 'with' as error and treat all types as dynamic types
because
	- it is disallowed in strict mode
	- general opinion is 'with' statement are dangerous
	- practical issues of determining the indentifiers that are in scope at compile time


### variable
->The first charecter must be one of the following:
	- uppercase
	- lowercase
	- undescore
	- dollar sign
	- unicode character from categories - Uppercase letter (Lu), Lowercase letter (Ll), Title case letter (Lt), Modifier letter (Lm), Other letter (Lo), or Letter number (Nl)

-> Subsequent characters follow the same rule and also allow the following:
	- numeric digits
	- a Unicode character from categories—Non-spacing mark (Mn), Spacing combining mark (Mc), Decimal digit number (Nd), or Connector punctuation (Pc)
	the Unicode characters U+200C (Zero Width Non-Joiner) and U+200D (Zero Width Joiner)

-> In JS it is possible to create a global variable by declaring it without the 'var' keyword, but in ts this is not allowed

## Types
-> typescript is optionally statically typed: types are checked automatically to prevent accidental assignments of invalid values

## Type Annotations
-> this is how we can make a type explicit either for safety or readability
 - var [identifier] : [type-annotation] = value ;
 - var [identifier] : [type-annotation]	;
 - var [identifier] = value;


