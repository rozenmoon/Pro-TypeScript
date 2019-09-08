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
because - it is disallowed in strict mode - general opinion is 'with' statement are dangerous - practical issues of determining the indentifiers that are in scope at compile time

### variable

->The first charecter must be one of the following: - uppercase - lowercase - undescore - dollar sign - unicode character from categories - Uppercase letter (Lu), Lowercase letter (Ll), Title case letter (Lt), Modifier letter (Lm), Other letter (Lo), or Letter number (Nl)

-> Subsequent characters follow the same rule and also allow the following: - numeric digits - a Unicode character from categories—Non-spacing mark (Mn), Spacing combining mark (Mc), Decimal digit number (Nd), or Connector punctuation (Pc)
the Unicode characters U+200C (Zero Width Non-Joiner) and U+200D (Zero Width Joiner)

-> In JS it is possible to create a global variable by declaring it without the 'var' keyword, but in ts this is not allowed

### Types

-> typescript is optionally statically typed: types are checked automatically to prevent accidental assignments of invalid values

### Type Annotations

-> this is how we can make a type explicit either for safety or readability

- var [identifier] : [type-annotation] = value ;
- var [identifier] : [type-annotation] ;
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

### Different between Type alias and Interface

-> Interface can be use to extend or implements clause. It can be used to when defining other interface and classes
-> Interface can also accept type arguments, making interface generic
-> Type alias can do neither of these

```
// Interface
interface PersonInterface {
    name: string;
    heightInCentimeters: number;
}
const sherlock: PersonInterface = {
    name: 'Bendict',
    heightInCentimeters: 183
}
// Type Alias
type PersonType = {
    name: string;
    heightInCentimeters: number;
};
const john: PersonType = {
    name: 'Martin',
    heightInCentimeters: 169
}
```

### Primitive types

-> The any type is exclusive to TypeScript and denotes a dynamic type. This type is used whenever TypeScript is unable to infer a type, or when you explicitly want to make a type dynamic.

-> three special type (not for type annotation but absence of values)

- 'undefiend' when not been assigned to a value
- 'null' intentional absence of an object value
- 'void' onln on function return type

### Enumerations

## -> Enumerations represent a collection of named elements that you can use to avoid littering your program with hard-coded values

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

-

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

### Bit flag

- enums are used to define bit flags
- the assigned values must follow the binary sequence, each value is a power of 2s

```
enum DiscFlags {
    None = 0,
    Drive = 1,
    Influence = 2,
    Steadiness = 4,
    Conscientiousness = 8
}
// Using flags
var personality = DiscFlags.Drive | DiscFlags.Conscientiousness;
// Testing flags
// true
var hasD = (personality & DiscFlags.Drive) == DiscFlags.Drive;
// false
var hasI = (personality & DiscFlags.Influence) == DiscFlags.Influence;
// false
var hasS = (personality & DiscFlags.Steadiness) == DiscFlags.Steadiness;
// true
var hasC = (personality & DiscFlags.Conscientiousness) == DiscFlags.Conscientiousness;
```

- the value assigned to each item can be constant or computed
- constant values are any expression that can be interpreted by type system, such as literal values , calculation and binary operators
- computed values are expressions that cannot be effetivly interpreted by compiler such string length or calling out method

### const Enumeraration

- created using the const keyword
- is erased during compilation and all code referring to it is replaced with hard-coded values

```
const enum VehicleType {
    PedalCycle,
    MotorCycle,
    Car,
    Van,
    Bus,
    Lorry
}
const type = VehicleType.Lorry;

var type = 5 /* Lorry */;
JavaScript output of a constant enumeration
```

- const enmunerator are not allowed to have computed members

### Union types

- Can be read by 'OR'
- It widens the allowable values

```
// Type annotation for a union type
let union: boolean | number;
// OK: number
union = 5;
// OK: boolean
union = true;
// Error: Type "string" is not assignable to type 'number | boolean'
union = 'string';
// Type alias for a union type
type StringOrError = string | Error;
// Type alias for union of many types
type SeriesOfTypes = string | number | boolean | Error;
```

- Consider using a type alias to reduce repetition
- Union type can be created using any types available not just primitive types

### Literal types

- Literal types can be used to narrow the range of allowable values to a subset of the type such as reducing a string to set of specific values

```
type Kingdom = 'Bacteria' | 'Protozoa' | 'Chromista' | 'Plantae' | 'Fungi' | 'Animalia';
let kingdom: Kingdom;
// OK
kingdom = 'Bacteria';
// Error: Type 'Protista' is not assignable to type 'Kingdom'
kingdom = 'Protista';
```

- Literal types are just union types made up of specific values, so number literal type or union/literal hybrid type can also be created using the same syntax

```
/ Number literal type
type Fibonacci = 1 | 2 | 3 | 5 | 8 | 13;
let num: Fibonacci;
// OK
num = 8;
// Error: Type '9' is not assignable to type 'Fibonacci'
num = 9;
// Hybrid union/literal type
type Randoms = 'Text' | 10 | false;
let random: Randoms;
// OK
random = 'Text';
random = 10;
random = false;
// Error: Not assignable.
random = 'Other String';
random = 12;
random = true;

```

### Intersection Type

- Its the opposit of Union type which means 'either A or B'. Intersection type means "both A and B".
- It uses ampersand sign and is read as 'AND'

```
interface Skier {
    slide(): void;
}
interface Shooter {
    shoot(): void;
}
type Biathelete = Skier & Shooter;

```

- It is usefull in 'mixins'

### Arrays

- To specify an array type, you simply add square brackets after the type name.
- Array<type>(long hand) or type[](short hand)

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

- this is allowed because 'status of liberty' object is compatible to Moment interface, this is called 'structural typing'

### Tuple Type

- Tuple type uses an array and specifies the type of elements based on its position

```
let poem: [number, boolean, string];
// OK
poem = [1, true, 'love'];
// Error: 'string' is not assignable to 'number'
poem = ['my', true, 'love'];

```

### Dictionary types

- we can represent dictionary in ts using index type
- index type specifies the key and its type in square brackets and the type of the value afterwards as type annotation
- The cephalopod dictionary is an object with dynamic keys, but TypeScript will ensure the types of the keys and values are correct.

```
let dictionary: CephalopodDictionary = {};
dictionary['octopus vulgaris'] = { hasInk: true, arms: 8, tentacles: 0 };
dictionary['loligo vulgaris'] = { hasInk: true, arms: 8, tentacles: 2 };
// Error. Not assignable to type 'Cephalopod'
dictionary[0] = { hasInk: true };
const octopus = dictionary['octopus vulgaris'];
// 0 (The common octopus has no tentacles)
console.log(octopus.tentacles);
// Remove item
delete dictionary['octopus vulgaris'];
```

### Mapped type

- it reduces the efforts to create similar types that differs only in optionality or readability
- it allows to create variations of exiting typre in a single expression
- it used `keyof` keyword which is an index type query that gathers a list of permitted property names for a type

```
interface Options {
    material: string;
    backlight: boolean;
}
// Manually created readonly interface
interface ManualReadonlyOptions {
    readonly material: string;
    readonly backlight: boolean;
}
// Manually created optional interface
interface ManualOptionalOptions {
    material?: string;
    backlight?: string;
}
// Manually created nullable interface
interface ManualNullableOptions {
    material: string | null;
    backlight: string | null;
}
```

becomes...

```
interface Options {
    material: string;
    backlight: boolean;
}
// Mapped types
type ReadOnly<T> = { readonly [k in keyof T]: T[k]; }
type Optional<T> = {[k in keyof T]?: T[k]; }
type Nullable<T> = {[k in keyof T]: T[k] | null; }
// Creating new types from mapped types
type ReadonlyOptions = Readonly<Options>;
type OptionalOptions = Optional<Options>;
type NullableOptions = Nullable<Options>;
```

### Discriminated Union

1. several type that share a common string literal property called a discriminant
2. A type alias for union of these types called a union
3. A type guard that checks the discriminant

```
interface Cube {
    kind: 'cube'; // Discriminant
    size: number;
}
interface Cuboid {
    kind: 'cuboid'; // Discriminant
    width: number;
    depth: number;
    height: number;
}
// Union
type Prism = Cube | Cuboid;
function volume(prism: Prism): number {
    // Type Guard
    switch (prism.kind) {
        case 'cube':
            return prism.size * prism.size * prism.size;
        case 'cuboid':
            return prism.width * prism.depth * prism.height;
        default:
            assertNever(prism);
            break;
    }
}
function assertNever(arg: never): never {
    throw new Error("Possible new tagged type: " + arg);
}

```

### Increment and Decrement

- it is applicable on `number`, `any` and `enum`
- if the `enum` goes out of range the undefined is returned

```
enum Size {
    S,
    M,
    L,
    XL
}
var size = Size.S;
++size;
console.log(Size[size]); // M
var size = Size.XL;
--size;
console.log(Size[size]); // L
var size = Size.XL;
++size;
console.log(Size[size]); // undefined
```


### Type assertions

-> Use only when you are sure of type
It overrides the type

```
interface House {
    bedrooms: number;
    bathrooms: number;
}

interface Mansion {
    bedrooms: number;
    bathrooms: number;
    butlers: number;
}

var avenueRoad: House = {
    bedrooms: 11,
    bathrooms: 10,
    butlers: 1
};

// Errors: Cannot convert House to Mansion
var mansion: Mansion = avenueRoad;

// Works
var mansion: Mansion = <Mansion>avenueRoad; -> here
```

-> although type assertion overrides the type but checks are still performed when type is assert, it is possible to do force a type assertion

```
var name: string = 'Avenue Road';

// Error: Cannot convert 'string' to 'number'
var bedrooms: number = <number> name;

// Works
var bedrooms: number = <number> <any> name;
```

### Type Guards

type guards is statements that results in the type becoming narrower.

```
function typeGuardExample(stringNumber: string | number) {
    // Error: Property does not exist
    const a = stringNumber.length;
    const b = stringNumber.toFixed();
    // this is Type guard
    if (typeof stringNumber === 'string') {
        // OK
        return stringNumber.length;
    } else {
        // OK
        return stringNumber.toFixed();
    }
}

```

we should make use of `typeof` and `instanceof` to check inside the function

NOTE:
The rules for determining the type resulting from a plus operation are

- If the type of either of the arguments is a string, the result is always a string.
- If the type of both arguments is either number or enum, the result is a number.
- If the type of either of the arguments is any, and the other argument is not a string, the result is any.
- In any other case, the operator is not allowed.

### Short-circuit Evaluation

-> as soon as statement can be answered evaluation resolved
-> ensure the value is defined before it is used

### Rest Parameters

- Only one rest parameter is allowed.
- The rest parameter must appear last in the parameter list.
- The type of a rest parameter must be an array type.

The function should expect to receive any number of argument including none of specified type.
The compiled js have map arguments list to your array variable within the body.

```
function getAverage(...a: number[]): string {
    let total = 0;
    let count = 0;
    for (let i = 0; i < a.length; i++) {
        total += a[i];
        count++;
    }
    const average = total / count;
    return 'The average is ' + average;
}
// 'The average is 6'
const result = getAverage(2, 4, 6, 8, 10);
```

- If you require that at least one argument is passed, you would need to add a required parameter before the rest parameter to enforce this minimum requirement.

### Destructuring

Allows you to unpack an array or object into named variable

```
const triangles = [1, 3, 6, 10, 15, 21];
// Destructuring
const [first, second] = triangles;
// 1
console.log(first);
// 3
console.log(second);
```

Rest parameters can also be used. it should appear at the last in the list and will receive all the values left

```
const triangles = [1, 3, 6, 10, 15, 21];
// Destructuring with a rest argument
const [first, second, ...remaining] = triangles;
// 1
console.log(first);
// 3
console.log(second);
// [6, 10, 15, 21]
console.log(remaining);
```

We can also skip an item in the array by leaving a blank space between the commas

```
const triangles = [1, 3, 6, 10, 15, 21];
// Skipping third item
const [first, second, , fourth] = triangles;
// 1
console.log(first);
// 3
console.log(second);
// [10]
console.log(fourth);
```

Swipping elements with destructing

```
[a,b] = [b,a]
```

Destructuring to unpack object:

```
const highSchool = { school: 'Central High', team: 'Centaurs' };
// Object destructuring
const { school: s, team: t } = highSchool;
// 'Central High'
console.log(s);
// 'Centaurs'
console.log(t);
```

We can also auto-unpack object if we use variable names that match the property names.

```
const highSchool = { school: 'Central High', team: 'Centaurs' };
// Auto-unpacking
const { school, team } = highSchool;
// 'Central High'
console.log(school);
// 'Centaurs'
console.log(team);
```

we can use rest parameter in object destructuring, it will result in an object containig all the properties that wasnt explicitly unpack

```
const pets = { cat: 'Pickle', dog: 'Berkeley', hamster: 'Hammy'}
// Object destructuring
const { dog, ...others } = pets;
// 'Berkeley'
console.log(dog);
//  Object { cat: 'Pickle', hamster: 'Hammy'}
console.log(others);
```

If the destructure past the avaiable values. the result will be undefined.

```
onst triangles = [1, 3, 6];
// Destructuring past available values
const [first, second, third, fourth] = triangles;
// undefined
console.log(fourth);

```

We can mitigate against undefined value by supplying default values

```
const triangles = [1, 3, 6];
// Destructuring past available values
const [first, second, third = -1, fourth = -1] = triangles;
// 6
console.log(third);
// -1
console.log(fourth);
```

### Spread Operator

Its the opposite of destructuring and can be used to pack arrays and objects using a shallow copy.
Spread operator works with properties but not methods
Its uses the rest parameter syntex

```
const squares = [1, 4, 9, 16, 25];
const powers = [2, 4, 8, 16, 32];
// Array spreading
const squaresAndPowers = [...squares, ...powers];
// [1, 4, 9, 16, 25, 2, 4, 8, 16, 32]
console.log(squaresAndPowers);
```

Object spreading
the syntex is same for object spreading as well. If same members appers on both objects the last assignment wins and overwrites any previous values

```
const emergencyService = {
    police: 'Chase',
    fire: 'Marshall',
};
const utilityService = {
    recycling: 'Rocky',
    construction: 'Rubble'
};
// Object spreading
const patrol = { ...emergencyService, ...utilityService };
// { police: 'Chase', fire: 'Marshall', recycling: 'Rocky', construction: 'Rubble' }
console.log(patrol);
```

### Function

```
function getAverage(a: number, b: number, c: number): string {
    var total = a + b + c;
    var average = total / 3;
    return 'The average is ' + average;
}

var result = getAverage(4, 3, 8); // 'The average is 5'
```

-> it is worth leaving out the return type unless the function returns no value. If you don’t intend to return a value, an explicit `void` type will prevent a return value being added to a function at a later date that could break the design

->

### Optional Parameters

Optional parameter required to be placed after requiered parameters.
`typeof` check is must as it might contain empty string or undefined

```
function getAverage(a: number, b: number, c?: number): string {
   let total = a;
   let count = 1;
   total += b;
   count++;
   if (typeof c !== 'undefined') {
       total += c;
       count++;
   }

```

### Default Parameters

```
function concatenate(items: string[], separator = ',', beginAt = 0, endAt = items.length) {
    let result = '';
```

The Js code generated by default parameters includes a `typeof` check

As check is moved inside the function body we can use wide range of runtime values as default values. not restricted to compile-time constants.

### Rest Parameters
Same as above

### Overload
- it is recomonded to write a seperate well named function that makes the intension explicit
- ts can overload all the overloads in a single implementation
The actual signature of the function appears last and is hidden by the overloads
- the final signature is called an implementation signature
- the implementation signature must define parameter and return value that are compatible with all the preceding signature
- the overload can have fewer parameter and also their type can be different but the implementation signature have to mark the extra parameters optional, default or rest parameters
- when the function with overload defined is called the compiler constructs a list of signature that matchs the function call, if no match the call results an error, if one or more matches the earlist of matching signature in the order they appear in the file determines the return type

```
function getAverage(a: string, b: string, c: string): string;
function getAverage(a: number, b: number, c: number): string;
// implementation signature
function getAverage(a: any, b: any, c: any): string {
    const total = parseInt(a, 10) + parseInt(b, 10) + parseInt(c, 10);
    const average = total / 3;
    return 'The average is ' + average;
}
// The average is 5
const result = getAverage(4, 3, 8);

```
- it creates an burden to the function as type may need to be tested or converted and they may cause multiple logical branches within the function
- simpler solution would be to use union type of `string | number` with a single funciton signature


 ### Specialized overload signatures
 - creating overload based on string constant rather than the overload being based on different parameters

 There are some rules to follow when using specialized overload signatures
1. There must be at least one nonspecialized signature.
2. Each specialized signature must return a subtype of a nonspecialized signature.
3. The implementation signature must be compatible with all signatures.

```
class HandlerFactory {
    getHandler(type: 'Random'): RandomHandler;
    getHandler(type: 'Reversed'): ReversedHandler;
    getHandler(type: string): Handler; // non-specialized signature
    getHandler(type: string): Handler { // implementation signature
        switch (type) {
            case 'Random':
                return new RandomHandler();
            case 'Reversed':
                return new ReversedHandler();
            default:
                return new Handler();
        }
    }
}
```
DId not understant the DOM element example

### Arrow functiom

ts compiler has option to target version 3 and version 5 of ECMAScripts specification and has support for new annual version such as ECMA2015 onwards.
Version 4 was abandoned
```
const shortAddNumbers = (a: number, b: number) => a + b;
const mediumAddNumbers = (a: number, b: number) => {
    return a + b;
}
const longAddNumbers = function (a: number, b: number) {
    return a + b;
}

```
- when using the first case -> when an object is returned { firstName: 'Mark', lastName: 'Rendle' } of object comfuses the compiler, in this case it should be wrapped by ({})

```
const makeName = (f: string, l: string) => ({ first: f, last: l });
```

- also use to prevent lexical scope of `this` keyword
- ts compiler creates `_this` just before the arrow fuction is defined and set its value to current value of this
- It also substitutes any usages of `this` within the function with the newly introduced `_this` variable, so the statement now reads `_this.text` in the JavaScript output.
- The use of the `_this` variable inside the function creates a closure around the variable, which preserves its context along with the function.
DId not understand this

### Function Currying
- We can hold onto the result of the first fuction call and use it many times is one of key point of currying

```
const multiply = (a: number) => (b: number) => a * b;
// Pass both arguments in sequence: 30
const numA = multiply(5)(6);
// Pass just the first argument and re-use
const orderOfMagnitude = multiply(10);
// 10
const deca = orderOfMagnitude(1);
// 100
const hecta = orderOfMagnitude(deca);
// 1,000
const kilo = orderOfMagnitude(hecta);
```
currying with overload

```
function multiply(a: number): (b: number) => number;
function multiply(a: number, b: number): number;
function multiply(a: number, b: number = null) {
    if (b === null) {
        return (b: number) => a * b;
    }
    return a * b;
}
// Pass both arguments "normally": 30
const numA = multiply(5, 6);
// Pass just the first argument and re-use
const orderOfMagnitude = multiply(10);
// 10
const deca = orderOfMagnitude(1);
// 100
const hecta = orderOfMagnitude(deca);
// 1,000
const kilo = orderOfMagnitude(hecta);
```
- if you are calling the function several times with same parameter consider using curring

### Interface
- Interface do not result in generation of any js due to type erasure
- Inteface are used at design time to provide autocompletion and at compile time to provide type checking
- Like enumerations, interface remain open and all the decalaration with a common root are merged into single structure
- can’t declare the same property in multiple blocks of the same interface "duplicate identifier” error will be thrown


