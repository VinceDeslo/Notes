# Typescript

## Basic Types:

```tsx
// numerals
let isDone: boolean = false;
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
let big: bigint = 100n;
// strings
let color: string = "blue";
let colors: string = `red and ${color}`;
// arrays
let list: number[] = [1, 2, 3];
let list: Array<number> = [1, 2, 3];
// tuples
let x: [string, number] = ["hello", 10];
```

## Enums:

```tsx
enum Color {
  Red,
  Green,
  Blue,
}
let c: Color = Color.Green; // value
let colorName: string = Color[2];   // name
```

## Unknowns:

```tsx
let notSure: unknown = 4;
notSure = "maybe a string instead";
notSure = false;

// checking them
if (notSure === true){...}
if (typeof notSure === "string"){...}
```

## Any (Loose Typing):

```tsx
let loose: any = 4;
// OK, ifItExists might exist at runtime
loose.ifItExists();
// OK, toFixed exists (but the compiler doesn't check)
loose.toFixed();
```

## No types:

```tsx
void : opposite of any -> absence of type
null : null like other languages
undefined: assignable to void variables similar to null

never :
// Function returning never must not have a reachable end point
function error(message: string): never {
  throw new Error(message);
}
```

## Object:

```tsx
// non primitive types
let o: object = {}

Object.keys(o) // Get keys
Object.values(o) // Get values

```

## Type Assertion (casting):

```tsx
let someValue: unknown = "this is a string";
let strLength: number = (someValue as string).length;   // as keyword
let strLength: number = (<string>someValue).length;     // angle bracket syntax
```

## Type Guards:

```tsx
if(typeof text === "string"){ ....}
```

## Union Types:

```tsx
function padLeft(value: string, padding: string | number) {
  // ... Padding is either a string or a number
}
```

## Common Union Fields:

```tsx
// Types are fixed
type NetworkLoadingState = {
  state: "loading";
};

type NetworkFailedState = {
  state: "failed";
  code: number;
};

type NetworkSuccessState = {
  state: "success";
  response: {
    title: string;
  };
};

// Create a type which represents only one of the above types
// but you aren't sure which it is yet.
type NetworkState = NetworkLoadingState  | NetworkFailedState  | NetworkSuccessState;

// Validate typing with a switch in further code
let state: NetworkState = new NetworkState()
```

## Intersection Types:

```tsx
// Interfaces are extendable
interface ErrorHandling {
  success: boolean;
  error?: { message: string };
}

interface ArtworksData {
  artworks: { title: string }[];
}

interface ArtistsData {
  artists: { name: string }[];
}

// This type contains all members of previous interfaces
type ArtworksResponse = ArtworksData & ErrorHandling & ArtistsData;

// Type extension with intersections
type ArtistsInfo = ArtistsData & {
  education: string
}
```

## Utility types:

```tsx
List of utility types:
ttps://www.typescriptlang.org/docs/handbook/utility-types.html

Partial<Type> // Constructs a type with all properties of Type set to optional.
Readonly<Type> // Constructs a type with all properties of Type set to readonly.
Record<Keys,Type> // Constructs a type whose prop keys are Keys and whose prop values are Type.
Pick<Type, Keys> // Constructs a type by picking the set of properties Keys from Type.
Omit<Type, Keys> // Constructs a type by picking all properties from Type and then removing Keys.
Exclude<Type, ExcludedUnion> // Constructs a type by excluding from Type all union members that are assignable to ExcludedUnion.
Extract<Type, Union> // Constructs a type by extracting from Type all union members that are assignable to Union.
NonNullable<Type>  // Constructs a type by excluding null and undefined from Type.
Parameters<Type> // Constructs a tuple type from the types used in the parameters of a function type Type.
ConstructorParameters<Type> // Constructs a tuple or array type from the types of a constructor function type.
ReturnType<Type> // Constructs a type consisting of the return type of function Type.
InstanceType<Type> // Constructs a type consisting of the instance type of a constructor function in Type.
Required<Type> // Constructs a type consisting of all properties of Type set to required.
ThisParameterType<Type> // Extracts the type of the this parameter for a function type
OmitThisParameter<Type> // Removes the this parameter from Type.
ThisType<Type> // This utility does not return a transformed type. Instead, it serves as a marker for a contextual this type.
```

## String methods:

```tsx
charAt()        // Returns the character at the specified index.
charcodeAt()    // Returns a number indicating the Unicode value of the character at the given index. (use with String.charCodeAt())
concat()        // Combines the text of two strings and returns a new string.
indexOf()       // Returns the index within the calling String object of the first occurrence of the specified value, or -1 if not found.
lastIndexOf()   // Returns the index within the calling String object of the last occurrence of the specified value, or -1 if not found.
localCompare()  // Returns a number indicating whether a reference string comes before or after or is the same as the given string.
match()         // Used to match a regular expression against a string.
replace()       // Used to find a match between a regular expression and a string, and to replace the match with a new substring.
search()        // Executes the search for a match between a regular expression and a specified string.
slice()         // Extracts a section of a string and returns a new string.
split()         // Splits a String object into an array of strings by separating the string into substrings.
substr()        // Returns the characters in a string beginning at the specified location through the specified number of characters.
substring()     // Returns the characters in a string between two indexes into the string.
toLocaleLowerCase() // The characters within a string are converted to lower case while respecting the current locale.
toLocaleUpperCase() // The characters within a string are converted to upper case while respecting the current locale.
toLowerCase()   // Returns the calling string value converted to lower case.
toUpperCase()   // Returns the calling string value converted to uppercase.
toString()      // Returns a string representing the specified object.
valueOf()       // Returns the primitive value of the specified object.
```

## Array methods:

```tsx
concat()        // Returns a new array comprised of this array joined with other array(s) and/or value(s).
every()         // Returns true if every element in this array satisfies the provided testing function.
filter()        // Creates a new array with all of the elements of this array for which the provided filtering function returns true.
forEach()       // Calls a function for each element in the array.
indexOf()       // Returns the first (least) index of an element within the array equal to the specified value, or -1 if none is found.
join()          // Joins all elements of an array into a string.
lastIndexOf()   // Returns the last (greatest) index of an element within the array equal to the specified value, or -1 if none is found.
map()           // Creates a new array with the results of calling a provided function on every element in this array.
pop()           // Removes the last element from an array and returns that element.
push()          // Adds one or more elements to the end of an array and returns the new length of the array.
reduce()        // Apply a function simultaneously against two values (from left-to-right) as to reduce it to a single value.
reduceRight()   // Apply a function simultaneously against two values (from right-to-left) as to reduce it to a single value.
reverse()       // Reverses the order of the elements of an array -- the first becomes the last, and the last becomes the first.
shift()         // Removes the first element from an array and returns that element.
slice()         // Extracts a section of an array and returns a new array.
some()          // Returns true if at least one element in this array satisfies the provided testing function
sort()          // Sorts the elements of an array.
splice()        // Adds and/or removes elements from an array.
toString()      // Returns a string representing the array and its elements.
unshift()       // Adds one or more elements to the front of an array and returns the new length of the array.
```

## Iterators:

```tsx
let list = [4, 5, 6];
// Only objects with the Symbol.iterator prop (for-of)
for (let i of list) console.log(i); // 4, 5, 6
// for-in returns keys and works on any object
for (let i in list) console.log(i); // "0", "1", "2"

```

## Decorators:

```tsx
// Attachable functions to a class declaration, method, accessor, property, or parameter.
function g() {
  console.log("g(): evaluated"); // call to the decorator itself
  return function (
    target,
    propertyKey: string,
    descriptor: PropertyDescriptor
  ) {
    console.log("g(): called"); // functionality of decorator
  };
}
```

## Iterators:

```tsx
let list = [4, 5, 6];
// Only objects with the Symbol.iterator prop (for-of)
for (let i of list) console.log(i); // 4, 5, 6
// for-in returns keys and works on any object
for (let i in list) console.log(i); // "0", "1", "2"

```

## Classes:

```tsx
// Definition
class Greeter {
  greeting: string; // property

  constructor(message: string) {    // constructor
    this.greeting = message;
  }

  greet() {
    return "Hello, " + this.greeting;   // method
  }
}
// Instanciation
let greeter = new Greeter("world");
```

## Inheritance:

```tsx
// Base
class Animal {
  move(distance: number = 0) {
    console.log(`Animal moved ${distanceInMeters}m.`);
  }
}
// Derived
class Dog extends Animal {
  constructor(name: string) {
    super(name); // permits usage of this with baseclass methods
  }
  // Added method
  bark() {
    console.log("Woof! Woof!");
  }
  // Method override
  move(distanceInMeters = 45) {
    console.log("Galloping...");
    super.move(distanceInMeters); // call to baseclass method
  }
}

const dog = new Dog(); // has .bark() and .move()
```

## Acces modifiers:

```tsx
// Applied to properties and methods
public name: string; //Accessible by everywhere (default)
private name: string; // Accessible only by base class
protected name: string; // Accessible by base class and derived classes
readonly name: string; // Does not permit assignment (must be initialized)
```

## Parameter properties:

```tsx
// Property initialized in constructor args (needs an access modifier)
class Octopus {
  public numberOfLegs: number = 8;
  constructor(public name: string) {} // parameter prop
}
let friend = new Octopus("Henry")
console.log(friend.name) // prints out Henry
```

## Accessors:

```tsx
class Employee {
  private _fullName: string = ""; // property to be accessed

  get fullName(): string {  // Getter method
    return this._fullName;
  }

  set fullName(newName: string) {   // Setter method
    if (newName && newName.length > 10) {
      throw new Error("fullName has a max length of " + 10);
    }

    this._fullName = newName;
  }
}
// Classes with a get and no set are infered as readonly
```

## Static props:

```tsx
// Properties applied on class and not on the instance
class Grid {
  static origin = { x: 0, y: 0 };   // static prop called with Grid.origin

  calculateDistanceFromOrigin(point: { x: number; y: number }) {
    let xDist = point.x - Grid.origin.x;    // call to static prop
    let yDist = point.y - Grid.origin.y;
    return Math.sqrt(xDist * xDist + yDist * yDist) / this.scale;
  }

  constructor(public scale: number) {}
}
```

## Abstract Classes:

```tsx
// Abstract classes cannot be instantiated, they only permit derivation
abstract class Department {
  constructor(public name: string) {}

  printName(): void {
    console.log("Department name: " + this.name);   // Standard method
  }

  abstract printMeeting(): void; // must be implemented in derived classes
}
```

## Constructor functions:

```tsx
class Greeter {
  greeting: string;

  constructor(message: string) { // the constructor takes a string
    this.greeting = message;
  }

  greet() {
    return "Hello, " + this.greeting; // the string is applied to the method
  }
}

let greeter: Greeter;       // we instanciate the object
greeter = new Greeter("world"); // and apply the constructor function
console.log(greeter.greet()); // "Hello, world"
```

## Generic functions:

```tsx
// any keyword looses type info when <T> keeps it. Type piping kinda
function identity<T>(arg: T): T {
  return arg;
}
// Using the generic
let output = identity<string>("myString"); // type is stated
let output = identity("myString");  // type is inferred
//       ^ = let output: string

// Permits usage of .length and array operations
function loggingIdentity<T>(arg: T[]): T[] {
  console.log(arg.length);
  return arg;
}
// Also written as with array generic type
function loggingIdentity<T>(arg: Array<T>): Array<T> {
  console.log(arg.length); // Array has a .length, so no more error
  return arg;
}
```

## Generic types:

```tsx
// Generic function used
function identity<T>(arg: T): T {
  return arg;
}

// Type of generic function is <T>(arg: T) value of T is a handle
let myIdentity: <T>(arg: T) => T = identity;
let myIdentity: <U>(arg: U) => U = identity; // Possible to change generic type parameter
let myIdentity: { <T>(arg: T): T } = identity; // Same thing but as a call signature literal

// moving the call literal to an interface
interface GenericIdentityFn {
  <T>(arg: T): T;
}
// We can assign its type like this
let myIdentity: GenericIdentityFn = identity;

// Make the type parameter visible
interface GenericIdentityFn<T> {
  (arg: T): T;
}
// It can now be used like this accepting all types
let myIdentity: GenericIdentityFn<number> = identity;
```

## Generic Classes:

```tsx
class GenericNumber<T> {
  zeroValue: T;
  add: (x: T, y: T) => T;   // method signature (like a macro in C)
}

// Instanciation
let stringNumeric = new GenericNumber<string>();
// Initializations
stringNumeric.zeroValue = "";
stringNumeric.add = function (x, y) {
  return x + y;
};
```

## Generic constraints:

```tsx
// Used for limiting the parameters accepted
interface Lengthwise {
  length: number;   // demands the implementation of .length
}

// Deriving a new generic from Lengthwise
function loggingIdentity<T extends Lengthwise>(arg: T): T {
  console.log(arg.length); // Now we know it has a .length property
  return arg;
}

loggingIdentity(3); // causes error cause no .length property
loggingIdentity([1,2,3]); // compiles

// This case extends with a generic parameter T
function getProperty<T, K extends keyof T>(obj: T, key: K) {
  return obj[key];
}

let x = { a: 1, b: 2, c: 3, d: 4 }; // this is the signature
getProperty(x, "a");    // a is present due to K extension
getProperty(x, "m");    // m is not and causes an error

console.log("Hello world")

function create<T>(c: { new (): T }(╯°o°）╯︵ ┻━┻: T {
  return new c();
}
```

## Factories with generics:

```tsx
// The type of C is a constructor of generic type
function create<T>(c: { new (): T }): T {
  return new c();
}

// Base class
class Animal {
  numLegs: number;
}
// Derived class
class Lion extends Animal {
  keeper: ZooKeeper;
}
// Factory using based class
function createInstance<A extends Animal>(c: new () => A): A {
  return new c();
}
// We can use a generic factory for all extensions of Animal
createInstance(Lion).keeper
```

---

# DOM manipulation:

```tsx
//HTMLElement
const app = document.getElementById("app");         // Fetch the main app div (can return null)
const p = document.createElement("p");              // Create a paragraph element (can create custom tags)
const div = document.getElementByTagName("div")[0]   // Fetches all matching tags and returns an array of them
p.textContent="Hello paragraph";                    // Initialize the text in the paragraph
app?.appendChild(p);                               // Make p a child of app (node extension)

app.children;   // HTMLCollection(2) [p, p]     // Contains only HTMLElement objects
app.childNodes; // NodeList(2) [p, p]           // Contains text also

querySelector();        // Returns first descendant of matching node
querySelectorAll();     // Returns all

<ul>
  <li>First :)</li>
  <li>Second!</li>
  <li>Third times a charm.</li>
</ul>;

const first = document.querySelector('li');     // Returns first list element
const all = document.querySelectorAll("li");    // Returns all list elements

```

---

# Data Structures:

## Stack:

```tsx
// Stack generic class to implement LIFO
class Stack<T> {
  _store: T[] = [];         // set local stack
  push(val: T) {            // Encapsulate JS .push method
    this._store.push(val);
  }
  pop(): T | undefined {    // Encapsulate JS .pop method (pops last)
    return this._store.pop();
  }
}
```

## Queue:

```tsx
// Queue generic class to implement FIFO
class Queue<T> {
  _store: T[] = [];         // set local stack
  push(val: T) {            // Encapsulate JS .push method
    this._store.push(val);
  }
  pop(): T | undefined {    // Encapsulate JS .shift method (pops first)
    return this._store.shift();
  }
}
```

## Binary Tree:

```tsx
// create node
interface TreeNode<T> {
    data: T,
    left?: TreeNode<T>,
    right?: TreeNode<T>,
    level?: number

    constructor(data: any[]) {
        this.data = data;
        this.left = undefined;
        this.right = undefined;
        this.level = undefined;
    }
}

// Items necessary
root: treeNode<T>
constructor() // Calls the initialization
init()  // runs create in a loop
create()  // Generates the nodes

// Traversals
- Pre order recursive (root - left - right)
- In order recursive traversal (left - root - right)
- Post order recursive traversal (left - right - root)

```

---

# Patterns:

## Singleton:

```tsx
class Singleton {
    static instance: Singleton = undefined;
    instanceID: number;

    // Initialization method of an instance
    init(id: number){
        this.instanceID = value;
        this.getInstance = () => Singleton.instance
    }

    // Determines if an instance exists
    constructor(id: number) {
        if(Singleton.instance === undefined){
            Singleton.instance = this.init(id); // Construction only if instance is not present
        }
        return Singleton.instance; // provide the instance
    }
}
// Assignment of the singleton
const inst1 = new Singleton(10);

```

## Factory:

```tsx
// Base class
class Product {
    name: string;
    price: number;

    constructor (...p: Array<any>){
        this.name = p[0];
        this.name = p[1];
    }
}
// Derived class
class Drink {
    ml: number;

    constructor (...p: Array<any>){
        super(p[0], p[1])
        this.ml = p[2];
    }
}

// Factory class
class ProductFactory {
    static create(type: string, ...rest) : Product {
        switch(type){
            case 'drink':
                return new Drink(...rest);
        }
    }
}

// Usage
const item = ProductFactory.create('drink', 'Nestea', 2.75, 700);

```

## Builder:

```tsx
// Base class
class Product {
    name: string;
    price: number;
    // Setter methods
    setName(name: string) {this.name = name;}
    setPrice(price: number) {this.price = price;}
}

// Builder class
class ProductBuilder {
    product: Product;
    constructor() {this.product = new Product();}

    // Setter wrappers
    setName(name: string) : ProductBuilder {
        this.product.setName(name);
        return this;
    }
    setPrice(price: number) : ProductBuilder {
        this.product.setPrice(price);
        return this;
    }
    // Instance Return function
    getProduct() : Product {return this.product}
}

// Construction and instanciation
const builder = new ProductBuilder();
builder.setName('Nestea').setPrice(2.75);
const drink = builder.getProduct();

```

---

# MATH STUFF

## factorial:

```tsx
// Recursive approach
var f = [];
function factorial (n) {
  if (n == 0 || n == 1) return 1;
  if (f[n] > 0) return f[n];
  return f[n] = factorial(n-1) * n;
}

// Iterative approach
var f = [];
function factorial(n) {
    while (n > 0) {
        f = f * n;
        n = n - 1;
    }
    return f;
}
```

## fibonacci:

```tsx
// Recursive approach
function fibonacci(num) {
    if (num < 1) return 0;
    if (num < 2) return 1;
    return fibonacci(num - 1) + fibonacci(num - 2);
}

// Iterative approach
function fibonacci(num){
  let a = 1, b = 0, temp;
  while (num >= 0){
    temp = a;
    a = a + b;
    b = temp;
    num--;
  }
  return b;
}
```

## Prime numbers:

```tsx
// Standard complexity O(n)
function isPrime(num) {
  for(var i = 2; i < num; i++)
    if(num % i === 0) return false;
  return num > 1;
}

// Lower time complexity O(sqrt(n))
const isPrime = num => {
    for(let i = 2, s = Math.sqrt(num); i <= s; i++)
        if(num % i === 0) return false;
    return num > 1;
}
```

## Splitting numbers into digits:

```tsx
// Convert to string and handle chars
let num = 12345;
let digitStrings = num.toString().split('')
let digits = digitStrings.map(n => +n)
```