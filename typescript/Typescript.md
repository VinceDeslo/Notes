# Typescript:

## Basic Types:

```typescript
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

```typescript
enum Color {
  Red,
  Green,
  Blue,
}
let c: Color = Color.Green;	// value
let colorName: string = Color[2];	// name
```

## Unknowns:

```typescript
let notSure: unknown = 4;
notSure = "maybe a string instead";
notSure = false;

// checking them
if (notSure === true){...}
if (typeof notSure === "string"){...}
```

## Any (Loose Typing):

```typescript
let loose: any = 4;
// OK, ifItExists might exist at runtime
loose.ifItExists();
// OK, toFixed exists (but the compiler doesn't check)
loose.toFixed();
```

## No types:

```typescript
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

```typescript
// non primitive types 
let o: object = {}
```

## Type Assertion (casting):

```typescript
let someValue: unknown = "this is a string";
let strLength: number = (someValue as string).length;	// as keyword
let strLength: number = (<string>someValue).length;		// angle bracket syntax
```

## Type Guards:

```typescript
if(typeof text === "string"){ ....}
```

## Union Types:

```typescript
function padLeft(value: string, padding: string | number) {
  // ... Padding is either a string or a number
}
```

## Common Union Fields:

```typescript
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

```typescript
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

```typescript
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







Casting:

```python

```

Lambdas (Anonymous functions):

```python

```

Decorators:

```python

```

Iterators:

```Python

```

Generators:

```Python

```

_____

# DATA STRUCTURES:

Stack:

```python

```



Queue:

```python

```



Binary Tree:

```Python


```



_____

# MATH STUFF



factorial:

```python

```

fibonacci:

```python

```

Prime numbers:

```python

```

Splitting numbers into digits:

```python

```

