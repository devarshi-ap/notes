# TypeScript



- **TS** is a syntactic superset of **JS** which adds **static typing**

- TLDR: **JS has a lot of BS**, **TS adds type safety**.

TypeScript uses compile time type checking. Which means it checks if the specified types match **before** running the code, not **while** running the code.

A common way to use **TS** is to use the official **TS Compiler**, which transpiled TS --> JS.

```bash
npm i typescript --save-dev
```

You can run the compiler with:

```bash
npx tsc
```

You can configure the TS compiler using a **tsconfig.json** file. It can be generated with:

```bash
npx tsc --init
```



The above is just one option to get started with TS; you can also use create-react-app then check off TS, etc...

- ```bash
  npx create-react-app <app_name> --template typescript
  ```

- ```bash
  npx create vite@latest <app_name> --template react-ts
  ```

- ```bash
  npm create-next-app@latest --ts
  ```



---

## Simple (Primitives) Types

There are three main primitives in JavaScript and TypeScript.

- **<u>`boolean`</u>** - true or false values
- <u>**`number`**</u> - whole numbers and floating point values
- **<u>`string`</u>** - text values



### Type Assignment

When creating a variable, there are 2 main ways to assign a type:

1. **<u>`Explicit`</u>** - writing out the type:

   - ```tsx
     let firstname: string = "Dev";
     ```

   - easier to read and more intentional

     

2. **<u>`Implicit`</u>** - TS will **infer** the type based on the assigned value:

   - ```tsx
     let firstname = "Dylan"
     ```

   - shorter, faster, and more often used when developing and testing



## Type Assignment Error

- TS will throw an error if data types don't match

  ```tsx
  // EXPLICIT
  let firstName: string = "Dev"; // string
  firstName = 19; // throws error: value is number
  
  // IMPLICIT
  let firstname = "Dev";
  firstname = 19 // still throws error
  ```

  

## Unable to Infer

- TS may not always properly **infer** the variable type.
- In such cases, it will set the type to **<u>`any`</u>**, which disables type checking



---

## Special Types

TS has special types that may not refer to any specific type of data.



### > Type: <u>any</u>

- type that disables type checking and allows all types to be used.

- ```tsx
  let x: any = true;
  x = "string"		// no error as it can be 'any' type
  Math.round(x) 	// same as above
  ```



### > Type: <u>unknown</u>

- similar, but safer alternative to **any**.

- TS will prevent **unknown** types from being used

- ```tsx
  let w: unknown = 1;
  w = "string"; // no error
  w = {
    runANonExistentMethod: () => {
      console.log("I think therefore I am");
    }
  } as { runANonExistentMethod: () => void}
  
  // How can we avoid the error for the code below when we don't know the type?
  w.runANonExistentMethod(); // Error: Object is of type 'unknown'. 
  ```

- best used when you don't know the type of data being typed.

- To add a type later, you'll need to cast it.

- Casting is when we use the "as" keyword to say property or variable is of the casted type



### > Type: <u>never</u>

- **never** effectively throws an error whenever it is defined.

- ```tsx
  // Error: Type 'boolean' is not assignable to type 'never'. 
  let x: never = true;
  ```



### > Type: <u>undefined & null</u>

- **`undefined`** and **`null`** are types that refer to the JS primitives **`undefined`** and **`null`**, respectively.

- ```tsx
  let y: undefined = undefined;
  let z: null = null; 
  ```



**<u>These types don't have much use unless `strictNullChecks` is enabled in the `tsconfig.json` file.</u>**    



----

## Arrays



For Explicit assignment, add a **[ ]** after the value type (number[ ], ...)

```tsx
const names: string[] = [];
names.push("Dev") // works just like JS array

// TS will throw type error for incompatable values
names.push(3) // can't push number to string[]
```



### Readonly

The **<u>*`readonly`*</u>** keyword can prevent arrays from being changed.

```tsx
const names: readonly string[] = ["Dev", "Nelly"]
names.push("Akon") // error
```



### Type Inference

TS can infer the array type based on its values

```tsx
const numbers = [1, 2, 3] // inferred to type: number[]
numbers.push("4") // error

// when reading values:
let firstNum: number = numbers[0];
```



----

## Tuples

array w/ a **pre-defined length** and **types** for **each index** and allow for **arrays with different types**, all of which are known.



#### Defining Tuple

- To define a tuple, specify the type of each element in the array:

```tsx
let myTup: [number, boolean, string]; // define types
myTup = [99, true, "HOV"] // initialize must correspond

myTup = [true, "HOV", 5] // ERROR; ORDER MATTERS
```

#### Readonly Tuples

- It is suggested to make tuples **readonly** since there's no type safety in the tuple outside the first n indexes with strongly defined types:

  ```tsx
  // We have no type safety in our tuple for indexes 3+
  let ourTuple: [number, boolean, string];
  ourTuple.push('4th index is not type safe');
  
  // Instead, use readonly
  let ourTuple: readonly [number, boolean, string] = [99, true, 'LP']
  ourTuple.push('4th index is not type safe'); // ERROR
  ```

#### Named Tuples

- **Named tuples** allow us to provide context for values at each index:

  ```tsx
  const graph: [x: number, y: number] = [55.2, 41.3]; 
  ```

#### Destructuring Tuples

- Since tuples = arrays, we can also destructor them:

  ```tsx
  const graph: [number, number] = [1, 2]; // new tuple
  const [x, y] = graph; // x=1, y=2
  ```

  

----



## Object Types

TS has specific syntax for Objects (python dictionaries). It basically adds a schema for each Object, allowing for inferences and type safety.

```tsx
const car: {
  // SCHEMA
  type: string,
  model: string,
  year: number
} = {
  // VALUES
  type: "Acura",
  model: "NSX",
  year: 2017
}; 

// TS infers types of properties, and will throw errors:
car.year = 2020 		// no err
car.year = "2020"		// err (year: number)
```



#### Optional Properties

- properties followed by a **?** don't have to be defined during Object definition.

  ```tsx
  // NO ERROR; 'mileage' is optional
  const car: { type: string, mileage?: number } = {
    type: "Toyota",
  };
  ```
  
  

#### Index Signatures

- When you don’t know all the **names of a type’s properties** ahead of time, but you do know the **shape of the values**, you can use an **index signature** to describe the **types of possible values**:

  ```tsx
  /*
  StringArray interface has the index signature, which states that when a StringArray is indexed with a number, it will return a string.
  
  An index signature property type must be string/number.
  */
  interface StringArray {
    [index: number]: string;
  }
   
  const myArray: StringArray = getStringArray();
  const secondItem = myArray[1];
  ```

---



## Enums

**enum** is a **special class** that represents a **group of 'const' variables**. They come in 2 flavours: **numeric** and **string**.



### 1. Numeric Enums

- **<u>Default Numeric Enums</u>**: where **enums** will initialize the **first value to 0** and **add 1** to each **additional value**:

  ```tsx
  enum myValues {
    A,  	// default 0
    B, 		// 1
    C, 		// 2
    D 		// 3
  }
  
  console.log(myValues.D); // 3
  ```

- **<u>Initialized Numeric Enums</u>**: where you set the value of the **first numeric enum**, and have it **auto increment** after that:

  ```tsx
  enum myValues {
    A = 99, // set 99
    B, 			// 100
    C, 			// 101
    D 			// 102
  }
  ```

- **<u>Fully Initialized Numeric Enums</u>**: where you set **unique numeric values for each enum value** (no auto increment)

  ```tsx
  enum myValues {
    A = 99,
    B = 89,
    C = 79,
    D = 69
  }
  ```



### 2. String Enums

```tsx
 enum Passwords {
	  Gmail = "abc123",
    Github = "abc789"
};

console.log(Passwords.Gmail); // "abc123"
```

---



TS allows **types to be defined separately** from the variables that use them. You can use **Aliases & Interfaces** to be easily shared b/n different variables/objects.



## Type Aliases

- doesn’t actually **create a new type** - it **creates a new *name*** to refer to that type.

  ```tsx
  // ex. Aliasing on Primitives (not really useful)
  type Second = number;
  let time: Second = 10; // same as::: let time: number = 10
  
  // ex. Aliasing on Complex types like Objects (helpful)
  
  type CarYear = number;
  type CarType = string;
  type isCarInsured = boolean;
  type Car = {
    year: CarYear; // number
    type: CarType; // string
    isInsured: isCarInsured; // boolean
  }
  
  // now you can use this 'Car' type for different Car objects
  const myCarYear: CarYear = 2001;
  const myCarType: CarType = "Sportscar";
  const isMyCarInsured: isCarInsured = true;
  const myCar: Car = {
    year: myCarYear,
    type: myCarType,
    isInsured: isMyCarInsured
  }
  
  console.log(myCar.year); // 2001
  console.log(myCar.type); // Sportscar
  console.log(myCar.isInsured); // true
  ```

  

## Interfaces 

- similar to type aliases, except they **only** apply to **OBJECTS**

  ```tsx
  interface Car {
      year: number,
      type: string,
      isInsured: boolean,
      isTinted?: boolean
  }
  
  let myCar: Car = {
      year: 2003,
      type: "Coupe",
      isInsured: true,
  }
  
  console.log(myCar.type); // Coupe
  ```

  

- **Interfaces can EXTEND other interfaces (union)** using the **extends** keyword:

  ```tsx
  nterface Rectangle {
    height: number,
    width: number
  }
  
  interface ColoredRectangle extends Rectangle {
    color: string
  }
  
  const coloredRectangle: ColoredRectangle = {
    height: 20,
    width: 10,
    color: 
  ```

---



## Union Types

- used when a **value can be > 1 type**

- using the **|** like: <type1> | <type2>, we are saying that _ is type1 or type2

  ```tsx
  // @param 'code' can be either string OR number (either works)
  function printStatusCode(code: string | number) {
    console.log(`My status code is ${code}.`)
  }
  printStatusCode(404); 		// WORKS
  printStatusCode('404');  	// WORKS
  
  // make sure that the code works fine for both type1 and type2; ie. don't call string functions on _ if _ may also be a number.
  ```
  

---



## Functions

TS has specific syntax for adding types to fx parameters & return values:

```js
// Note: TS will infer types if they're not explicit

// syntax
function <myFunc>(<param>: <type>): <returnType> {
	return ...      
}

{/* Void Return Type*/}
const sayHi = (name: string): void => {
	console.log(name)      
}

{/*Optional? + Default= Parameters*/}
function addNums(a: number, b?: number = 1): number {
  return a + b;
}


{/*Rest Parameters (type must be array)*/}
function add(a: number, b:number, ...rest: number[]) {
  return a + b + rest.reduce((p, c) => p + c, 0);
}
```



### Export & Import Functions

- Use **named exports** (unlimited exports in a file):

  ```js
  export function sayHi(): void {
    ...
  }
    
  // to import:
  import {sayHi} from './path2file'
  ```

- Use **default exports** (1 per file):

  ```js
  export default function sayHi(): void {
    ...
  }
    
  // to import:
  import sayHi from './path2abovefile'
  ```

- If you have a file that does **1 default export** & **many named exports**:

  ```js
  // 👇️ default export
  export default function sum(a: number, b: number): number {
    return a + b;
  };
  
  // 👇️ named export
  export const example = 'hello world';
  
  // in another file, to import:
  import sum, { example } from './path2abovefile'
  ```

---



## Function Overloading

- **Overloading** - same name, different parameters and return types

- Method 1:

  ```tsx
  function greet(person: string | string[]): string | string[] {
      if (typeof person === 'string') {
        	return `Hello, ${person}!`;
      } else if (Array.isArray(person)) {
        	return person.map(name => `Hello, ${name}!`);
      }
  }
  
  greet('World');		// 'Hello, World!'
  greet(['Dev', 'Bruce']);		// ['Hello, Dev!', 'Hello, Bruce!']
  ```

  

- Method 2: Define so-called *<u>overload signatures</u>* & an *<u>implementation signature</u>*

  - overload signatures don't have a body; they only define params & their types
  - the implementation signature has a body **and** defines params & their types

  ```jsx
  // Overload signatures (unlimited)
  function greet(person: string): string;
  function greet(persons: string[]): string[];
   
  // Implementation signature (only 1)
  function greet(person: unknown): unknown {
      if (typeof person === 'string') {
        	return `Hello, ${person}!`;
      } else if (Array.isArray(person)) {
        	return person.map(name => `Hello, ${name}!`);
      }
  }
  
  greet('World');		// 'Hello, World!'
  greet(['Dev', 'Bruce']);		// ['Hello, Dev!', 'Hello, Bruce!']
  ```

  

---

## Casting

- allows you to convert a variable from 1 type to another.

  

  ### Casting w/ <u>***as***</u>

  ```tsx
  let x: unknown = 'hello';
  console.log((x as string).length);
  
  
  // CASTING DOESN'T CHANGE THE TYPE OF THE DATA IN THE VARIABLE
  let x: unknown = 4;
  console.log((x as string).length); // err (x still holds number)
  
  
  // TO FORCE CAST, CAST TO 'UNKNOWN'
  let x = 'hello';
  console.log(((x as unknown) as string).length); // x is not actually a number so this will return undefined 
  ```

  ### Casting w/ ***<>***

  ```tsx
  // WONT WORK IN .TSX (REACT) !!!
  
  let x: unknown = 'hello';
  console.log( (<string>x).length );
  ```

---



## Basic Generics

Suppose you have an array; 'A' list of items. You don't know what the items are nor do you care. This means that you have an array of **generic** A elements. What A is is IRRELEVANT.

Many DS&A **do not depend on the *actual type* of the object**. However, you still want to enforce a constraint between various variables. Ie. a list reversal algorithm:

```tsx
/*
Here you are basically saying that reverse() takes an array (items: T[]) of some type T (notice the type parameter in reverse<T>) and returns an array of type T (notice : T[]). 
*/

function reverse<T>(items: T[]): T[] {
    let toreturn = [];
    for (let i = items.length - 1; i >= 0; i--) {
        toreturn.push(items[i]);
    }
    return toreturn;
}

// ie. passing number[] to reverse() will result in return type number[] 
var sample = [1, 2, 3];
var reversed = reverse(sample);
console.log(reversed); // [ 3, 2, 1 ]


// ie. passing string[] to reverse() will result in return type string[] 
var strArr = ['1', '2', '3'];
var reversedStrs = reverse(strArr);
console.log(reversedStrs); // [ '3', '2', '1' ]
```



### Type Aliases (and also for Interface)

Generics in type aliases allow creating types that are more reusable.

```tsx
type Wrapped<T> = { value: T };
const wrappeddNum: Wrapped<number> = { value: 10 };
const wrappeddStr: Wrapped<string> = { value: 'Ten' };
```



### Default Value

Generics can be assigned default values which apply if no other value is specified or inferred.

```tsx
// default value for Generic = string (type for _value variable which is set by the user)
class NamedValue<T = string> {
    private _value: T | undefined;

    constructor(private name: string) {}

    public setValue(value: T) {
      	this._value = value;
    }

    public getValue(): T | undefined {
      	return this._value;
    }

    public toString(): string {
      	return `${this.name}: ${this._value}`;
    }
}

let value = new NamedValue('myNumber');
value.setValue('myValue');
console.log(value.toString()); // myNumber: myValue
```



### Extends

Constraints can be added to generics to limit what's allowed

```tsx
// v1 must be type S=String/Number
// v2 must be type T=String/Number

function createPair<S extends string | number, T extends string | number>(v1: S, v2: T): [S, T] {
  console.log(`creating pair: v1='${v1}', v2='${v2}'`);
  return [v1, v2];
}
```

---



## Utility Types

TS comes with a large number of types that can help with some common type manipulation, usually referred to as **utility types**.

### Partial

- all the properties in an object are now <u>**optional**</u>.

  ```tsx
  interface Point {
    x: number;
    y: number;
  }
  
  let pointPart: Partial<Point> = {}; // x and y are optional
  pointPart.x = 10;
  console.log(pointPart);	// { x: 10 }
  ```

  

### Required

- all the properties in an object are now **<u>required</u>**.

  ```tsx
  interface Car {
    make: string;
    model: string;
    mileage?: number; // mileage is optional here, but Required<Car> makes it required
  }
  
  let myCar: Required<Car> = {
    make: 'Ford',
    model: 'Focus',
    mileage: 12000 // `Required` forces mileage to be defined
  };
  ```



### Record

- shortcut to defining an object type with a **<u>specific key type and value type</u>**.

  ```tsx
  // Record<string, number> ======= { [key: string]: number }
  
  const nameAgeMap: Record<string, number> = {
    'Alice': 21,
    'Bob': 25
  };
  ```

  

### Omit

- **<u>removes keys</u>** from an object

  ```tsx
  interface Person {
    name: string;
    age: number;
    location?: string;
  }
  
  const bob: Omit<Person, 'age' | 'location'> = {
    name: 'Bob'
    // Omit<Person> has removed age & location from Person type thus they can't be defined here
  };



### Pick

- **removes all but the specified keys** from an object

  ```tsx
  interface Person {
    name: string;
    age: number;
    location?: string;
  }
  
  const bob: Pick<Person, 'name'> = {
    name: 'Bob'
    // Pick<Person, 'name'> has only kept name, so age & location were removed from Person type thus they can't be defined here
  };
  ```

  
