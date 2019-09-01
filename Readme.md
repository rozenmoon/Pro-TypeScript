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

### Types
-> typescript is optionally statically typed: types are checked automatically to prevent accidental assignments of invalid values

### Type Annotations
-> this is how we can make a type explicit either for safety or readability
 - var [identifier] : [type-annotation] = value ;
 - var [identifier] : [type-annotation]	;
 - var [identifier] = value;
 -> 'any' opt-out of static type checking, which makes variable type dynamic

 ```
 // primitive type annotation
var name: string = 'Steve';
var heightInCentimeters: number = 182.88;
var isActive: boolean = true;

// array type annotation
var names: string[] = ['James', 'Nick', 'Rebecca', 'Lily'];

// function annotation with parameter type annotation and return type annotation
var sayHello: (name: string) => string;

// implementation of sayHello function
sayHello = function (name: string) {
    return 'Hello ' + name;
};

// object type annotation
var person: { name: string; heightInCentimeters: number; };

// Implementation of a person object
person = {
    name: 'Mark',
    heightInCentimeters: 183
};
```

-> we can use 'interface' when the type becomes too complex
```
interface Person {
    name: string;
    heightInCentimeters: number;
}

var person: Person = {
    name: 'Mark',
    heightInCentimeters: 183
}
```

### Primitive types
-> The any type is exclusive to TypeScript and denotes a dynamic type. This type is used whenever TypeScript is unable to infer a type, or when you explicitly want to make a type dynamic.

-> three  special type (not for type annotation but absence of values)
- 'undefiend'  when not been assigned to a value
- 'null' intentional absence of an object value
- 'void' onln on function return type

### Arrays
-> To specify an array type, you simply add square brackets after the type name.
-> Array<type> or type[]

```
interface Monument {
    name: string;
    heightInMeters: number;
}

// The array is typed using the Monument interface
var monuments: Monument[] = [];

// Each item added to the array is checked for type compatibility
monuments.push({
    name: 'Statue of Liberty',
    heightInMeters: 46,
    location: 'USA'
});
```
-> this is allowed because 'status of liberty' object is compatible to Moment interface, this is called 'structural typing'

### Enumerations
-> Enumerations represent a collection of named elements that you can use to avoid littering your program with hard-coded values
->
 ```
enum VehicleType {
    PedalCycle,
    MotorCycle,
    Car,
    Van,
    Bus,
    Lorry
}

var type = VehicleType.Lorry;

var typeName = VehicleType[type]; // 'Lorry'
```

->
```
enum BoxSize {
    Small,
    Medium
}

//...

enum BoxSize {
    Large = 2,
    XLarge,
    XXLarge
}
```