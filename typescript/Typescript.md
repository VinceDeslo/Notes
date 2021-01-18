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

## Type Assertion:

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

