# JavaScript

* Iterables

## DATA TYPES

* Number (decimals and whole numbers)
* BigInt (x > +/- 2^53 -1 )
* String
* Boolean
* Null (ie. let age = null;)
* Undefined (ie. let age;)
* Object (arrays etc...)
* Symbols (unique identifiers for objects)
* `typeof x` or `typeof (x)` returns a string with the name of the data type of x. For null, it returns "object".

***

## INTERACTION

* _**alert("Hello");**_ - shows a message and waits for the user to press "OK".
* _**result = prompt(title, \[default]);**_ - input field for user and buttons OK/Cancel. _title_ is text to show, _default_ is optional 2nd argument for initial value for the input field. \[]'s around default means its optional. The input is stored into result.
* _**result = confirm(question);**_ - shows text _question_ and has two buttons (Ok and Cancel) returns Boolean value.

***

## TYPE CONVERSIONS

* **String Conversion** - String(value);
* **Numeric Conversion** - Number(value);
  * undefined becomes NaN, null becomes 0, true becomes 1, false becomes 0, empty strings are 0.
* **Boolean Conversion** - Boolean(value);
  * 0 null indefined Nan "" become false. Any thing other than previous is true.

***

## BASIC OPERATORS

* **Operand** - what operators are applied to (ie. 5 \* 2 where 5 and 2 are operands and \* is the operators)
* _**Unary Operator**_ - operator and single operand ( x = -x )
  * Unary + : doesn't do anything to numbers but if operand isn't a number, it converts it to a number (+true is 1, +"2" is 2 as a number.)
  * Prefix Form: ++a : returns new incremented value
  * Postfix Form: a++ : returns old value before increment
* _**Binary Operator**_ - operator and 2 operands ( x - y )
* Other operators: +, -, \*, /, %, \*\* exponents (2\*\*3 = 8).

***

## COMPARISONS

`>,>=, <, <=, ==, !=`

* String Comparison - 'Z' > 'A' is true - compares lexicographical order where a is least Z is most in value.
* _**Strict Equality**_ : 0 == false is true b/c different types are converted to numbers by the equality operator `==`. So an "" becomes 0 as does false. `===` is the strict equality operator which checks equality without type conversion.

***

## IF-STATEMENT, ? OPERATOR

* The if, if-else, and if-elseif-else is the same as in Java
* _**? Operator**_
  *   Used to assign something to a variable depending on a condition:

      ```js
      if (age> 18) {
          pass = true;
      } else {
          pass = false;
      }

      // same thing but with ? operator:
      let pass = (age > 18) ? true : false;

      // general syntax
      let result = condition ? value1IfTrue: value2IfFalse;
      ```
  *   Multiple ?'s for >1 conditions:

      ```js
      let result = (condition) ? value1 :
      	(condition2) ? value2 :
      	(condition3) ? value3 :
      	value4Else;
      ```

***

## LOGICAL OPERATORS

* || OR
  * Finds first truthy value: `result = value1 || value2 || value3;` converts operands (value1/2/3) to Boolean and evaluates each from left to right one by one. If the operand is `true`, stops and returns the original value of that operand. if all are false, returns last operand.
* && AND
  * Finds the first falsy value. same process as above. If all are true, returns the last operand.
* ! NOT

***

## NULLISH COALESCING OPERATOR - ??

* ?? is the nullish coalescing operator; it treats null and undefined similarly and it's a nice syntax to get the first "defined" value of the two arguments.
* `a ?? b` --> returns the first argument (a) if it's not null/undefined; otherwise returns b. It's basically:

```js
result = (a !== null && a!== undefined) ? a : b;
```

* Multiple ??'s:

```js
// returns first of a/b/c which is defined (not null/undefined) otherwise "None".
a ?? b ?? c ?? "None";
```

***

## LOOPS

* while, do-while, for, switch, break/continue are all the same as in Java.

***

## FUNCTIONS

*   **Function Declaration**

    ```js
    function sayHi(name) {
        console.log(`"Hi ${name}"`);
    }
    ```
*   _**Default Parameters**_ - if an _actual parameter_ isn't provided, the _formal parameter_ is undefined. To bypass this:

    ```js
    function foo(param1, param2="no text given") {
        ...
    }
    ```
*   _**Return**_ - same as in Java. If a function has an empty `return` or doesn't have it at all, it returns `undefined`.

    ```js
    function doNothing() {
        return;
    }
    console.log( doNothing() === undefined ); // true
    ```

***

## FUNCTION EXPRESIONS

In JS, functions aren't structures; they're actually a special kind of value which can be assigned; hence _Function Expressions_:

```js
// function declaration
function sayHi() {
    console.log("hi");
}


// function expression
let sayHi = function() {
    console.log("hi");
};
```

The function is created and assigned to the sayHi variable. You can even **copy** a function to another variable:

```js
function sayHi() {console.log("hi");} 	// function expression would also work instead of this.
let func = sayHi;

func(); 	// hi
sayHi(); 	// hi
```

Differences b/n function expressions & declarations:

* Function Declaration:
  * function, declared as a separate statement, in the main code flow.
  * visible in the whole script, no matter where it is; can be called earlier than it's defined.
* Function Expression:
  * function, created inside an expression.
  * created when the execution reaches it and is usably only from that moment forward.

***

## ARROW FUNCTIONS

* There's another way to create functions besides declarations & expressions: Arrow Functions.

```js
// general syntax
let func = (arg1, arg2, ..., argN) => expression

let sum = (a, b) => a + b; 	// returns sum

// for 0 parameters:
let func = () => {...};
                  
// for 1 param, remove ():
let func = param1 => {...};
```

*   For a multiline expression, use {}'s and use a normal `return` inside them:

    ```js
    let sum = (a, b) => {
        let result = a + b;
        return result;
    };
    ```
* Arrow Functions:
  * Don't have `this`
  * Don't have `arguments`
  * Can't be called with `new`
  * Don't have `super`

***

## POLYFILLS

* New language features may include not only syntax constructs and operators, but also built-in functions. Ie. some outdated JS engines don't have Math.trunc() so it can't run that code.
*   A polyfill is a script which updates/adds new functions. It "fills" in the gap and adds missing implementations. (core.js is good for this)

    ```js
    if (!Math.trunc) {	/// if no such function,
        //implement it
        Math.trunc = function(number) {
            return number < 0 ? Math.ceil(number) : Math.floor(number);
        };
    }
    ```

## TRANSPILERS

* A transpiler is a special piece of software that can parse ("read and understand") modern code, and rewrite it using older syntax constructs (the result would be the same). Usually, a developer runs the transpiler on their own computer, and then deploys the transpiled code to the server. Babel is one of the most used transpilers.

***

## OBJECTS ; \[python dictionary]

* The `object` data type is basically the python dictionary. It's created with _{}'s_ and an optional list of _properties_
* _**`property`**_ is a key-value pair.
* _**`key`**_ is a string (called name/identifier)
* _**`value`**_ is anything
*   #### CREATE EMPTY OBJECT

    ```
    // 2 ways of creating an empty object

    let user = new Object();	// "object constructor" syntax
    let user = {};			   	// "object literal" syntax
    ```
*   #### LITERALS AND PROPERTIES

    ```js
    // This object has 3 properties
    let user = {
        // key: value,
        name: "John",
        age: 30,
        "likes birds": true, // multiword property name must be quoted
    };
    ```
*   #### ADD, REMOVE, AND READ

    ```js
    // GET property values of object using dot notation:
    var x = user.name;		// John
    var y = user.age;		// 30
    // dot notation won't work for multi-word properties so do this:
    var z = user["likes birds"];	// true

    // ADD value:
    user.isAdmin = true;

    // CHANGE value:
    user.age = 18;	// changes age to 18.
    user.age += 1;	// increments age by 1.

    // REMOVE property using 'delete _propertyName_':
    delete user.age;
    ```
*   #### PROPERTY VALUE SHORTHAND

    ```js
    function makeUser(name, age) {
        return {
            name: name,
            age: age,
        };
    }

    // SHORTHAND: instead of 'name: name,' just write 'name,'
    function makeUser(name, age) {
        return {
            name,		// same as name: name,
            age; 30,
        }
    }
    ```
*   #### PROPERTY EXISTENCE TEST, " in " OPERATOR

    ```js
    // check if a property exists in an object; returns boolean value.
    console.log("name" in makeUser);	// true
    ```
*   #### FOR-IN LOOP

    ```js
    // to iterate thru all keys in an object, use a for-in loop.
    let user = {name: "Dev", age: 17, isIndian: true};

    for(let key in user) {
        console.log( key );			// keys
        console.log( user[key] );	// values
    }
    ```
*   #### METHOD SHORTHAND

    ```
    // you can also add function expressions into objects then call those methods via dot notation:
    let user = {
        // method shorthand
        sayHi() {
            console.log("hi");
        }
    };
    ```
*   #### ' THIS ' METHODS

    ```js
    // used to access a property-value in a method, in the same Object:
    let user = {
        name: "Dev",
        age: 17,
        
        sayHi () {
            console.log(`"Hi ${this.name}"`);
        }
    };

    user.sayHi(); // Hi Dev
    ```
* #### CONSTRUCTOR FUNCTION - ' new ' operator
  *   They're technically regular functions, but they're always: 1) named with a capital letter first, and 2) they should be executed only with the `new` operator.

      ```js
      function User(name, age) {
          this.name = name;
          this.age = age;
          this.isAdmin = false; 
      }

      let user1 = new User("Dev", 17);		// [java: create User obj user1]

      console.log(user1.name);		// Dev
      console.log(user1.age);			// 17
      console.log(user1.isAdmin);		// false
      ```
* #### OBJECT TO PRIMITIVE CONVERSION
  * When objects are added/subtracted (obj1 +/- obj2) or printed, objects are auto-converted to primitives, then the operation is carried out.
  * Objects are `true` in boolean, and there are only numeric and string conversions
    * _`NUMERIC CONVERSION`_ - happens when you apply math functions on objects. ie. `Date` objects (from datetime) can be substracted
    * _`STRING CONVERSION`_ - happens when you output an object like alert(obj), etc...
    * **ToPrimitive**
      * There are 3 variants of type-conversion, each called a "hint":
      *   _Object-to-String_

          ```js
          alert(obj);		// output
          ```
      *   _Object-to-Number_

          ```js
          let num = Number(obj);	// explicit conversion
          let delta = date1 - date2;	// subtraction of datetime objects is allowed
          let greater = user1 > user2;	// less/greater comparison
          ```
      *   _Default_ - when operator is "not sure" what type to expect (ie. a + can concatenate sting && add nums)

          ```js
          let total = obj1 + obj2;	// binary plus uses "default"
          if (user == 1) {...};		// obj == number uses "default"
          ```
    *   **Symbol.toPrimitive**

        ```js
        obj[Symbol.toPrimitive] = function(hint) {
            // must return a primitive value
            // hint = one of "string", "number", "default"
        };

        // ex.
        let user = {
            name: 'dev',
            age: 17,
            [Symbol.toPrimitive](hint) {
                alert(`"hint: ${hint}"`);
                return hint == "string" ? `{name: "${this.name}"}` : this.age;
            }
        };

        // conversions demo:
        alert(user) // hint: string -> {name: "John"}
        alert(+user) // hint: number -> 17
        alert(user + 1) // hint: default -> 18
        ```
  *   Object.keys, .values, .entries

      ```js
      /*
      Object.keys(obj) 		- returns an array of keys
      Object.values(obj) 		- returns an array of values
      Object.entries(obj) 	- returns an array of [key, value] pairs
      */

      // looping over values (or keys):
      let salaries = {
          "john": 100,
          "pete": 300,
          "mary": 250
      };

      for (let salary of Object.values(salaries)) {
          // salary is values in salaries object
      }
      ```

***

* #### SYMBOL type
  * Object property keys can be either _Strings_ or _Symbols_.
  *   A Symbol is a unique value; It's created using `Symbol();`

      ```js
      // CREATE SYMBOL w/ an optional description (called symbol name/label)
      let id = Symbol("id");
      let id2 = Symbol("id");

      // SET a VALUE
      user[id] = "Their id value";

      // Set SYMBOL VALUE in an object LITERAL with square brackets but you still have to declare it as a symbol:
      let id = Symbol();
      let user = {
          name : "dev",
          [id] : 123
      };

      // id != id2 even though they share the same description/name.
      // for printing, either do:
      console.log(id.toString());		// shows 'symbol: id'
      console.log(id.description());	// shows 'description: id'
      ```
  * _**HIDDEN PROPERTIES**_ - symbols allow us to create hidden properties of an object that can't be accidentally access or overwrite. Symbols are skipped by `for-in` loops and `Object.keys(objectName)` method
  * _**GLOBAL SYMBOLS**_
    * Sometimes, you want same-names symbols, perhaps different parts of your application want to access symbol "id"- exactly the same property. That's where the _global symbol registry_ steps in. You can create symbols in it and access them later.
    *   In order to read a symbol from the registry, use `Symbol.for(key)`. This returns the symbol with the symbol name/description/label of _key_- otherwise, it creates a new symbol `Symbol(key)` and stores it:

        ```js
        // read from the global registry
        let id = Symbol.for("id");	// if the symbol doesn't exist, create it

        // read it again (maybe from another part of the code)
        let idAgain = Symbol.for("id");

        // the same symbol
        alert( id === idAgain );	// true

        // Symbol.keyFor(symbol) returns global symbol description
        let sym = Symbol.for("name");
        let sym2 = Symbol.for("id");

        alert( Symbol.forKey(sym) );	// name
        alert( Symbol.forKey(sym2) );	// id
        ```

***

## NUMBER

```js
// More ways to write a number:
let billion = 1000000000;
let billion = 1_000_000_000;
let billion = 1e9;
let ms = 1e-6;		// 0.000001 (microsecond)

// rounding: Math.floor, .ceil, .round, .trunc, and .toFixed(x) for nearest xth decimal
let numVar = 12.3494;
alert( numVar.toFixed(1) )		// 12.4

// parseInt/parseFloat "read" a number from a string from left to right until they can't:
alert( parseInt("100px") );		// 100
alert( parseFloar("12.5vw") );	// 12.5
alert( parseInt("a123") );		// NaN, the first symbol stops the process

// Max and min:
alert( Math.max(3, 5, -10, 0, 1) );		// 5
alert( Math.min(1, 2, 0) );			   // 0
```

***

## STRING

#### Concatenation

* ```js
  alert('wu' + '-tang')	// 'wu-tang'
  alert('1' + 2 + 2)		// '122' and not '14'
  ```

#### Length

* ```js
  'hello'.length	// 5
  ```

#### Finding String in a String

* ```js
  var str = "Please locate where 'locate' occurs!";	// -1 if not found

  var pos = str.indexOf("locate");			// pos=7
  var lastpos = str.lastIndexOf("locate");	// pos=21
  var posAfterIndex15 = str.indexOf("locate", 15);	// pos=21
  var pos = str.search("locate");		// pos=7

  // search() can't take a second start position argument
  // indexOf() can't take powerful search values (regex)
  ```

#### Substring (str.slice, str.substring, str.substr)

* ```js
  var str = "Apple, Banana, Kiwi";

  var res = str.slice(7, 13);		// Banana -> slice(include, exclude)
  var res = str.slice(-12, -6);	// Banana -> start @ end of str
  var res = str.slice(7);			// from 7 to end of str

  str.substring(7, 13); // same as slice, but can't do neg. params

  str.substr(7, 6);	// Banana -> 2nd param is length of substr (from 7, a 6 letter str)
  str.substr(-4);		// Kiwi -> counts backwards from end of str
  ```

#### Replacing String Content

*   replaces specified value with another value in a string. It doesn't change the string, it returns a new string. It only replaces _first match_ and is case sensitive.

    ```js
    str = "Please visit Microsoft";
    var n = str.replace("Microsoft", "Apple");		// n= "Please visit Apple"

    // to replace case insensitive, use /i flag:
    var n = str.replace(/MICROSOFT/i, "Apple");		// /i for insensitive

    // to replace all matches, use /g flag:
    var n = str.replace(/Microsoft/g, "Apple");		// /g for global
    ```

#### Upper and Lower Cases

* ```js
  str.toUpperCase();
  str.toLowerCase();
  ```

#### Trim

* ```js
  str.trim();		// removes whitespace from both sides of a string
  ```

#### Converting String to Array

* ```js
  str.split("");	// split string into all characters array
  str.split(",");	// split on commas
  ```

#### String interpolation (kinda like printf)

* ```js
  // use `` instead "" and insert variable into ${}
  let myPet = "chimp";
  console.log(`I own a pet ${myPet}.`)
  ```

#### Special Characters

* ```js
  let names = "Guests:\n * John\n * Pete\n * Mary";

  /*
  newline		\n
  quotes		\', \"
  backslash	\\
  tab			\t
  */
  ```

#### Loop Over characters with For-of Loop

* ```js
  for (let char of "hello") {
      console.log(char);		// H, e, l, l, o (char becomes H, then e, then l...)
  }
  ```

#### Test for Match (includes, startsWith, endsWith)

* ```js
  alert( "Widget with id".includes("Widget") );	// true
  alert( "Hello".includes("Bye") );			   // false

  // The opt. 2nd arg of str.includes is the position to start search:
  alert( "Widget".includes("id") );	// true
  alert( "Widget".includes("id", 3) );	// false [from position 3]
  ```

***

## ARRAYS

*   Creating an array

    ```js
    var cars = ["Corvette", "Alfa Romeo", "BMW"];
    var values = ["Foo", "Bar", 10];	// can hold multiple types

    // use names to access its "members"; person.firstName -> "John"
    var person = {firstName: "John", lastName: "Doe", age:46};
    ```
*   Access Elements

    ```js
    var firstCar = cars[0];
    var john = person.firstName;	// from person array
    ```
*   Adding Elements

    ```js
    var fruits = ["Banana", "Orange", "Apple", "Mango"];

    fruits.push("Lemon");			    // adds to end and returns length
    fruits[fruits.length] = "Peach";	// add peach at end
    ```
* _**Difference b/n Arrays & Objects**_: arrays use numbered indexes, while, Objects use names indexes.
*   Removing Elements

    ```js
    var nums = [1, 2, 3, 4];

    nums.pop();			// returns and removes last element
    nums.shift();		// removes first element and shifts element left by 1
    nums.unshift(1);	// adds new element in front, and pushes elements right by 1
    delete nums[0];		// change first element to undefined; leaves undefined "holes"
    ```
* Changing Elements and Copying Array
  * ```js
    cars[0] = "Ferrari";
    let copyCars = cars;		// copys entire array
    // typeof cars --> 'Object'
    ```
* Length (bit tricky)
  * ```js
    /* length is actually not the count of values in the array, but the greatest numeric index plus one. The length property is also writable. If we increase it manually, nothing interesting happens. But if we decrease it, the array is irreverseibly truncated: */

    let arr = [1, 2, 3, 4, 5];

    arr.length = 2; // truncate to 2 elements
    alert( arr ); // [1, 2]

    arr.length = 5; // return length back
    alert( arr[3] ); // undefined: the values do not return


    // so technically, the simplest way to clear an array is:
    arr.length = 0;
    ```
* Properties & Methods
  * ```js
    /*
    - length -> cars.length;
    - sort -> cars.sort();
    - reverse() -> reverses the array then returns it
    - check array -> Array.isArray(cars);
    - convert array to csv string -> cars.toString();
    - join elements by a char -> cars.join("*");

    - merge arrays -> arr3 = arr1.concat(arr2); adds arr2 at the end of arr1

    - slice part of array -> var x = nums.slice(1);		starts from 1 to end (do 1,x)

    - push(...items) –> adds items to the end,
    - pop() –> extracts an item from the end,
    - shift() –> extracts an item from the beginning,
    - unshift(...items) –> adds items to the beginning.
    - includes(value) -> returns boolean if array has the value.

    */
    ```
*   Iteration

    ```js
    let arr = ["Apple", "Orange", "Pear"];
      
    // normal for-loop:
    for (let i = 0; i < arr.length; i++) {
    	alert( arr[i] );
    }

    // for-of:
    for (let fruit of fruits) {
    	alert( fruit );
    }

    // for-in, since arrays are objects:
    for (let key in arr) {
    	alert( arr[key] ); // Apple, Orange, Pear
    }

    // for-each, run a function for elements in array:
    arr.forEach((item, index, array) {
    	alert( item );
    });

    ["Bilbo", "Gandalf", "Nazgul"].forEach((item, index, array) => {
    	alert(`${item} is at index ${index} in ${array}`);
    });
    ```
*   _**Multi-Dimensional Array**_

    ```js
    let matrix = [
        [1, 2, 3],
        [4, 5, 6],
        [7, 8, 9]
    ];

    // [row][column]
    alert( matrix[0][2] );	// 3
    ```
* _**.map()**_
  * allows you to run a function on each item in the array, returning a new array as the result
  *   In React, `map()` can be used to generate lists

      ```jsx
      const myArray = ['apple', 'banana', 'orange'];

      const myList = myArray.map((item) => <p>{item}</p>)
      ```

***

## MAP

* Basically an object (or python Dictionary) but Map allows keys of any type.
*   Methods and Properties:

    ```js
    /*
    new Map() 				– creates the map.
    map.set(key, value) 	– stores the value by the key.
    map.get(key) 			– returns value of key, else, undefined.
    map.has(key) 			– returns boolean if key exists.
    map.delete(key) 		– removes the value by the key.
    map.clear() 			– removes everything from the map.
    map.size 				– returns the current element count.
    map.keys() 				– returns an iterable for keys,
    map.values() 			– returns an iterable for values,
    map.entries() 			– returns an iterable for [key, value]'s.

    Every map.set returns the map, so we can chain the calls:

    map.set('1', 'str1')
    	 .set(1, 'num1')
       .set(true, 'bool1');
    */
    ```
*   Basic Implementation:

    ```js
    let map = new Map();		// creates the map

    map.set('name', 'dev');   // a string key
    map.set(99, 'problems');     // a numeric key
    map.set(true, 'isMessiGoat'); // a boolean key

    // Objects would convert keys to string but
    // Map keeps the type, so these two are different:
    alert( map.get('name') ); 		// 'dev'
    alert( map.get(99) );			// 'problems'
    alert( map.size ); 				// 3
    ```
*   Map can also use Objects as Keys:

    ```js
    let john = { name: "John" };
    let ben = { name: "Ben" };

    // for every user, let's store their visits count
    let usersMap = new Map();

    // john is the key for the map
    usersMap.set(john, 123);
    usersMap.set(ben, 321)

    alert( usersMap.get(john) ); // 123
    alert( usersMap.get(ben) ); // 321
    ```
*   Iteration

    ```js
    let recipeMap = new Map([
      ['cucumber', 500],
      ['tomatoes', 350],
      ['onion',    50]
    ]);

    // iterate over keys using map.keys()
    for (let vegetable of recipeMap.keys()) {
      alert(vegetable); // cucumber, tomatoes, onion
    }

    // iterate over values using map.values()
    for (let amount of recipeMap.values()) {
      alert(amount); // 500, 350, 50
    }

    // iterate over [key, value] entries.
    // recipeMap is the same as of recipeMap.entries()
    for (let entry of recipeMap) {
      alert(entry); // cucumber,500 (and so on)
    }

    // Map also has a built-in forEach method like the array:
    // runs the function for each (key, value) pair
    recipeMap.forEach( (value, key, map) => {
      alert(`${key}: ${value}`); // cucumber: 500 etc
    });
    ```

***

## SET

* “set of values” (without keys), where each value may occur only once
*   Methods & Properties:

    ```js
    /*
    new Set(iterable) 		– creates set- optional iterable object (array etc...)

    set.add(value) 			– adds a value, returns set.
    set.delete(value) 		– removes the value.
    set.has(value) 			– returns boolean if the value exists.
    set.clear() 			– removes everything from the set.
    set.size 				– is the elements count.

    *** main feature is that repeated calls of set.add(value) with the same value don’t do anything.
    */
    ```
*   Basic Implementation:

    ```js
    let set = new Set();		// creates set

    let john = { name: "John" };	// 3 users
    let pete = { name: "Pete" };	
    let mary = { name: "Mary" };

    // users are added, often repeatedly
    set.add(john);
    set.add(pete);
    set.add(mary);
    set.add(john); // repeat
    set.add(mary); // repeat

    alert( set.size ); // 3; set keeps only unique values

    for (let user of set) {
      alert(user.name); // John then Pete then Mary
    }
    ```
*   Iteration over Set:

    ```js
    let set = new Set(["oranges", "apples", "bananas"]);

    // single-line for-of loop
    for (let value of set) {
    	alert(value)
    }

    // forEach:
    set.forEach((value, valueAgain, set) => {
      alert(value);
    });
    ```

***

### WeakMap

* is `Map`-like collection that allows only objects as keys and removes them together with associated value once they become inaccessible by other means.

### WeakSet

* is `Set`-like collection that stores only objects and removes them once they become inaccessible by other means. \[WeakMap\&Set]'s main advantages are that they have weak reference to objects, so they can easily be removed by garbage collector. That comes at the cost of not having support for `clear`, `size`, `keys`, `values`…

***

## DESTRUCTURING ASSIGNMENT

* _Destructuring assignment_ is a special syntax that allows us to “unpack” arrays/objects into a bunch of variables.
*   #### Array Destructing

    ```js
    // we have an array with the name and surname
    let arr = ["John", "Smith"]

    // destructuring assignment
    // sets firstName = arr[0]
    // and surname = arr[1]
    let [firstName, surname] = arr;

    alert(firstName); 	// John
    alert(surname);  	// Smith
    ```

    *   Ignore Elements using commas

        ```js
        // second element is not needed so leave it empty
        let [firstName, , title] = ["Julius", "Caesar", "Consul"];

        alert( firstName );		// Julius
        alert( title ); 		// Consul
        ```
*   #### String Destructing

    ```js
    // destructive assignment can work on any iterable like strings
    let [a, b, c] = "abc"; 	// ["a", "b", "c"]
    let [one, two, three] = new Set([1, 2, 3]);	// even on Sets
    ```

    *   Assign to anything

        ```js
        // you can use any "assignables" on the left side.
        // Ie. an object property:
        let user = {};
        [user.name, user.surname] = "Julius Caesar".split(" ");
        alert(user.name);			// Julius
        alert(user.surname);	// Caesar
        ```
    *   Swapping Values in 1 line via destructive assignment

        ```js
        let user1 = "Julius";
        let user2 = "Pompey";
        [user1, user2] = [user2, user1];
        // now, user1="Pompey"	& 	user2="Julius"
        ```
    *   The Rest "..."

        ```js
        // Usually, if the array is longer than the list at the left, the “extra” items are omitted. If we’d like also to gather all that follows, add "...rest":

        let [name1, name2, ...rest] = ["A", "B", "C", "D", "E"];

        // 'rest' is array of items, starting from the 3rd one:
        // ["C", "D", "E"]
        alert(rest[0]); 		// C
        alert(rest.length); // 3

        // *** We can use any other variable name in place of rest 
        ```
    *   Default Value

        ```js
        // If the right array is shorter than the left list, they're just undefined values. If we want a “default” value to replace undefined values, we can provide it using =:
        let [name = "Guest", surname = "Anonymous"] = ["Julius"];

        alert(name);    // Julius (from array)
        alert(surname); // Anonymous (default used)
        ```
* #### Object Destructing
  * Basic Syntax: let {var1, var2} = {var1:…, var2:…}
  *   The right side is an existing object. The left side contains an object-like “pattern” for corresponding properties (same name as property names in object):

      ```js
      let options = {
        title: "Menu",
        width: 100,
        height: 200
      };

      let {title, width, height} = options;
      alert(title);  // Menu
      alert(width);  // 100
      alert(height); // 200

      // The order does not matter. This works too:
      let {height, width, title} = { title: "Menu", height: 200, width: 100 }
      ```
  *   If we want to assign a property to a variable with another name, set the variable name using a colon:

      ```js
      let {width: w, height: h, title} = options;
      ```
  *   The Rest "..."

      ```js
      let options = {title: "Menu", height: 200, width: 100};

      // rest = object with the rest of properties
      let {title, ...rest} = options;

      // now title="Menu", rest={height: 200, width: 100}
      alert(rest.height);  // 200
      alert(rest.width);   // 100
      ```

***

## DATE AND TIME

*   new Date object:

    ```js
    // no parameters
    let now = new Date();
    alert( now ); // shows current date/time

    /* new Date(year, month, date, hours, minutes, seconds, ms)

    - Create the date with the params (first 2 args are obligatory)
    - The year must have 4 digits.
    - The month count starts with 0 (Jan), up to 11 (Dec).
    - The date param is day of month, if absent then 1 is assumed.
    - If hours/min/secs/ms is absent, they're assumed to be 0.
    */
    new Date(2011, 0, 1, 0, 0, 0, 0); // 1 Jan 2011, 00:00:00
    new Date(2011, 0, 1); // the same, hours etc are 0 by default
    ```
*   Access date components from Date object:

    ```js
    /*
    getFullYear()		- get the year (4digits)
    getMonth()			- get month (from 0 to 11)
    getDate()				- Get the day of month, from 1 to 31
    --> getHours(), getMinutes(), getSeconds(), getMilliseconds()
    getDay()				- Get day of week, from 0 (Sun) to 6 (Sat)
    getTime()				- Returns timestamp (#ms since Jan,1,1970)
    */
    ```
*   Autocorrection (Out-of-range date components are distributed automatically)

    ```js
    let date = new Date(2016, 1, 28);
    date.setDate(date.getDate() + 2);

    alert( date ); // 1 Mar 2016
    ```
*   Date.now() - returns the current timestamp

    ```js
    let start = Date.now(); // ms count from 1 Jan 1970

    for (let i = 0; i < 100000; i++) {
      let doSomething = i * i * i;
    }

    let end = Date.now(); // done

    alert(`loop time (ms): ${end - start}`);
    ```
*   Date.parse() from a string

    ```js
    // The method Date.parse(str) can read a date from a string.
    // The string format should be: YYYY-MM-DDTHH:mm:ss.sssZ

    let ms = Date.parse('2012-01-26T13:51:50.417-07:00');
    alert(ms); // 1327611110417  (timestamp)
    ```

***

## JSON

* Let’s say we have a complex object, and we’d like to convert it to a string, to send it over a network, or just to output it for logging purposes. Throughout development, properties are added, renamed, and removed; updating a toString() every single time is PAIN.
* `JSON (JavaScript Object Notation)` is a general format to represent values/objects.
* #### JSON.stringify
  *   converts objects into JSON to a string called `encoded` / `serialized` / `stringified` / `marshalled` object.

      ```js
      let student = {
          name: 'John',
          age: 30,
          isAdmin: false,
          courses: ['java', 'py', 'js'],
          wife: null
       };
        
      let json = JSON.stringify(student);

      alert(typeof json); // we've got a string!

      alert(json);
      /* JSON-encoded object:
      {
          "name": "John",
          "age": 30,
          "isAdmin": false,
          "courses": ["html", "css", "js"],
          "wife": null
      }
      */
      ```

      Note: JSON-encoded object differs from the object literal in that:

      * Strings use `""`. No `''` or backticks in JSON. So `'John'`--> `"John"`.
      * All Object property names are `""`. So `age:30` --> `"age":30`.
      *   `JSON.stringify` can be applied to str, numbers, bool, `null`, & even arrays:

          ```js
          // a number in JSON is just a number
          alert( JSON.stringify(1) ) // 1

          // a string in JSON is still a string, but double-quoted
          alert( JSON.stringify('test') ) // "test"
          alert( JSON.stringify(true) ); // true
          alert( JSON.stringify([1, 2, 3]) ); // [1,2,3]
          ```
      *   JSON is a data-only language-independent specification, so some JS-specific object properties are skipped by `JSON.stringify`: functions, symbolic keys and values, and properties that store `undefined`:

          ```js
          let user = {
            sayHi() { // ignored
              alert("Hello");
            },
            [Symbol("id")]: 123, // ignored
            something: undefined // ignored
          };

          alert( JSON.stringify(user) ); // {} (empty object)
          ```
* #### JSON.parse
  *   To decode a JSON-string, we need JSON.parse(). Basic Syntax:

      ```js
      let value = JSON.parse(str, [reviver]);
      // str: JSON-string to parse
      /// reviver: Optional function(key,value) that will be called for each (key, value) pair and can transform the value
      ```
  *   Basic Implementation + For Nested Objects:

      ```js
      let numbers = "[0, 1, 2, 3]";		// stringified array
      numbers = JSON.parse(numbers);	// decodes from JSON
      alert( numbers[1] ); 						// 1

      // nested objects (ie. array property or another obj):
      let userData = '{ "name": "John", "age": 35, "isAdmin": false, "friends": [0,1,2,3] }';

      let user = JSON.parse(userData);		// decodes along with array obj
      alert( user.friends[1] ); 					// 1
      ```
  *   Reviver:

      ```js
      // Imagine, we got a stringified meetup object from the server:
      // title: (meetup title), date: (meetup date)
      let str = '{"title":"Meeting","date":"2017-11-30T12:00:00.000Z"}';

      /* PROBLEMOOO:
      let meeting = JSON.parse(str);		// deserialize

      // The value of meeting.date is a string, not a Date object.
      alert( meetup.date.getDate() );
      */

      // Pass to JSON.parse the reviving function as the second argument, that returns all values “as is”, but date will become a Date:

      let meeting = JSON.parse(str, function(key, value) {
        if (key == 'date')
          return new Date(value);
        return value;
      });

      alert( meetup.date.getDate() ); // now works!
      ```

***

## REST PARAMETERS

*   A function can be called with any number of arguments, no matter how it is defined:

    ```js
    function sum(a, b) {
      return a + b;
    }

    alert( sum(1, 2, 3, 4, 5) );	// 3
    // There's no "excessive arguments" error; only the first 2 count
    ```
*   The rest of the unused parameters can be included in the function definition by using three dots `...` followed by the name of the array that will contain them:

    ```js
    function sumAll(...args) { 	// args is the array
      let sum = 0;
      for (let arg of args) sum += arg;
      return sum;
    }
    alert( sumAll(1) ); 			// 1
    alert( sumAll(1, 2) ); 			// 3
    alert( sumAll(1, 2, 3) ); 		// 6
    ```
*   We can choose to get the first parameters as variables, and gather only the rest. Here below, the first 2 arguments go into variables, and the rest go into a 'titles' array:

    ```js
    function showName(firstName, lastName, ...titles) {
      alert( firstName + ' ' + lastName ); 		// Julius Caesar

      // i.e. titles = ["Consul", "Imperator"]
      alert( titles[0] ); // Consul
      alert( titles[1] ); // Imperator
      alert( titles.length ); // 2
    }

    showName("Julius", "Caesar", "Consul", "Imperator");
    ```

## Spread Syntax

* In Rest Parameters, we saw how to get an array from the list of parameters. But sometimes we need to do the opposite.
* Ie. Math.max() returns the greatest number from a list. Let's say we have an array \[3, 5, 1]. You can't pass the array into the function as it expects numeric arguments, and doing Math.max(arr\[0], arr\[1], etc..) may take forever.
*   `Spread Syntax` works similarly with rest parameters, also using `...`, but inversely. When ...arr is used in a function call, it expands the iterable object into the list of arguments:

    ```js
    let arr = [3, 5, 1];
    alert( Math.max(...arr) ); // 5 (spread turns arr into list of args)

    // we can also pass multiple iterables and solo number arguments:
    let arr2 = [8, 3, -8, 1];
    alert( Math.max(..arr, ...arr2, 8, 24) );		// 24
    ```
*   We can also use Spread Syntax to merge arrays:

    ```js
    let arr = [3, 5, 1];
    let arr2 = [8, 9, 15];
    let merged = [0, ...arr, 2, ...arr2];
    alert(merged); // 0,3,5,1,2,8,9,15 (0, then arr, then 2, then arr2)
    ```

***

## GLOBAL OBJECTS

* The Global object provides variables & functions that are available anywhere. In a browser it's named `window`. for Node.js it's `global`, and recently, `globalThis` (use this now).
*   In a browser, global functions & variables declared with `var` (not `let/const`) become the property of the global object:

    ```js
    var gVar = 5;
    alert(window.gVar); // 5 (became a property of the global object)
    ```
*   If a value is so important that you’d like to make it available globally, write it as a property:

    ```js
    window.currentUser = {
      name: "John"
    };

    // somewhere else in code
    alert(currentUser.name);  // John

    // or, if we have a local variable with the name "currentUser"
    // get it from window explicitly (safe!)
    alert(window.currentUser.name); 	// John
    ```
*   For some reason, this works instead of the above:

    ```js
    gVar = 5;
    console.log(global.gVar);	// 5
    ```

***

## NFE : Named Function Expression

In JS, functions are objects, kinda like: "action objects"

*   The "name" property:

    ```js
    // function’s name is accessible as the “name” property
    function sayHi() { alert("Hi"); }
    alert( sayHi.name ); // sayHi

    // also applicable to functions in Objects:
    let user = {
      sayHi() {/* ...*/},
      sayBye: function() {/* ...*/}
    }
    alert(user.sayHi.name); 	// sayHi
    alert(user.sayBye.name); 	// sayBye
    ```
*   The "length" property:

    ```js
    // returns the number of function parameters (excl. rest @params)
    function f1(a) {}
    function f2(a, b) {}
    function many(a, b, ...more) {}

    alert(f1.length); // 1
    alert(f2.length); // 2
    alert(many.length); // 2
    ```
*   _**NFE**_

    ```js
    // ordinary function expression:
    let sayHi = function(who) {
      alert(`Hello, ${who}`);
    };

    // add a name to it
    let sayHi = function func(who) {
      alert(`Hello, ${who}`);
    };

    // the "func" allows the function to reference itself internally, and it's not visisible outside the function:
    let sayHi = function func(who) {	// who is a param
      if (who) {
        alert(`Hello, ${who}`);
      } else {
        func("Guest"); // use func to re-call itself
      }
    };

    sayHi(); // Hello, Guest
    func(); // Error, func is not defined outside sayHi()
    ```
*   You can also call `sayHi()` internally and it would work, the problem is that `sayHi` may change outside. If the function gets assigned to another variable instead, the code will start to give errors:

    ```js
    let welcome = sayHi;
    sayHi = null;		// sayHi and welcome both point to the same thing
    welcome(); // Error, the nested sayHi call doesn't work any more!
    ```

***

## Function Binding

* When passing object methods as callbacks, there’s a known problem: "losing `this`".
*   ie. Here’s how it may happen with `setTimeout`:

    ```js
    let user = {
      firstName: "John",
      sayHi() {
        alert(`Hello, ${this.firstName}!`);
      }
    };

    setTimeout(user.sayHi, 1000); // Hello, undefined!

    // It outputs undefined instead of "John" for this.firstName because setTimeout got the function user.sayHi, separately from the object.
    ```
*   Solution: a Wrapper (also called wrapping function):

    ```js
    let user = {
      firstName: "John",
      sayHi() {
        alert(`Hello, ${this.firstName}!`);
      }
    };

    setTimeout(() => user.sayHi(), 1000); // Hello, John!
    // this works bc it recieves user from the outer lexical env, then calls the method normally.
    ```

***

## PROPERTY FLAGS AND DESCRIPTORS

* Object properties, besides a **`value`**, have three special attributes (“flags”):
  * **`writable`** – if `true`, the value can be changed, otherwise it’s read-only.
  * **`enumerable`** – if `true`, then listed in loops, otherwise not listed.
  * **`configurable`** – if `true`, the property can be deleted and these attributes can be modified, otherwise not.
  *   All 3 are initially `true`, but they can be changed. To access the full info about a property: (returns a "property-descriptor" object: value and all the flags)

      ```
      let descriptor = Object.getOwnPropertyDescriptor(obj, propertyName);
      ```
  *   Basic Implementation

      ```js
      let user = {
        name: "John"
      };

      let descriptor = Object.getOwnPropertyDescriptor(user, 'name');

      alert( JSON.stringify(descriptor, null, 2 ) );
      /* property descriptor:
      {
        "value": "John",
        "writable": true,
        "enumerable": true,
        "configurable": true
      }
      */
      ```
  *   To change the flags: use the `Object,defineProperty` method:

      ```js
      Object.defineProperty(obj, propertyName, descriptor)
      // descriptor: property descriptor object to apply
      ```
  *   Basic Implementation of _Writable_:

      ```js
      // make user.name non-writable (can’t be reassigned) by changing writable flag
      let user = { name: "John" };

      Object.defineProperty(user, "name", {
        writable: false
      });

      user.name = "Pete";		// Error; 'name' is read-only
      ```
  *   Basic Implementation of _Enumberable_:

      ```js
      // basically, the toString is skipped if enumerable is false
      let user = {
        name: "John",
        toString() { return this.name; }
      };

      Object.defineProperty(user, "toString", {
        enumerable: false
      });

      // Now our toString disappears:
      for (let key in user) alert(key); // name
      // non-enumerable properties are also skipped in Object.keys
      ```
  *   Basic Implementation of _Configurable_:

      ```js
      // basically, non-configurable =can't be deleted, nor can it be changed back with defineProperty (one-way road).
      // Below, user.name can't changed nor deleted.
      let user = {
        name: "John"
      };

      Object.defineProperty(user, "name", {
        writable: false,
        configurable: false
      });

      // won't be able to change user.name or its flags
      // all this won't work:
      user.name = "Pete";
      delete user.name;
      Object.defineProperty(user, "name", { value: "Pete" });
      ```
  *   Define many properties with Object.defineProperties:

      ```js
      // basic syntax:
      Object.defineProperties(obj, {
        prop1: descriptor1,
        prop2: descriptor2
        // ...
      });

      // ie.
      Object.defineProperties(user, {
        name: { value: "John", writable: false },
        surname: { value: "Smith", writable: false },
        // ...
      });
      ```

## PROPERTY GETTERS + SETTERS

* There are 2 kinds of object properties: `data properties`,`accessor properties`.
  *   _**Accessor**_ properties are essentially properties used to _get_ and _set_ a value. In an object literal, they're denoted by `get`and `set`:

      ```
      let obj = {
        get propName() {
          // getter, the code executed on getting obj.propName
        },

        set propName(value) {
          // setter, the code executed on setting obj.propName = value
        }
      };
      ```
  *   Basic implementation:

      ```js
      let user = {
        name: "John",
        surname: "Smith",

        get fullName() {		// getter
          return `${this.name} ${this.surname}`;
        },

        set fullName(value) {		// setter
          [this.name, this.surname] = value.split(" ");
        }
      };

      user.fullName = "Alice Cooper";		// set fullName splits this str
      alert(user.name); 				// Alice
      alert(user.surname); 			// Cooper
      ```
  *   You can also create accessor properties, get\&set, via defineProperty descriptor:

      ```js
      let user = {
        name: "John",
        surname: "Smith"
      };

      Object.defineProperty(user, 'fullName', {
        get() {
          return `${this.name} ${this.surname}`;
        },

        set(value) {
          [this.name, this.surname] = value.split(" ");
        }
      });

      alert(user.fullName); // John Smith
      for(let key in user) alert(key); // name, surname
      ```

***

## PROTOTYPAL INHERITANCE

* Java Inheritance (extending one object to another, to access object properties)

### \[ \[ Prototype ] ]

* Objects have a special hidden property \[\[Prototype]] ; either null or references another object. This object is called a "prototype".
* When we read a property from `object`, and it’s missing, JavaScript automatically takes it from the prototype. This is `Prototypal Inheritence`.
* The property `[[Prototype]]` is internal and hidden. One way to set it is:
  *   `__proto__`:

      ```js
      let animal = {
        eats: true
      };
      let rabbit = {
        jumps: true
      };

      rabbit.__proto__ = animal; // rabbit prototypically inherits from animal.

      // If we read a property from rabbit, and it’s missing, JS will automatically take it from animal:

      alert( rabbit.eats ); // true
      alert( rabbit.jumps ); // true
      ```
*   So if `animal` has a lot of useful properties and methods, then they become automatically available in `rabbit`. Such properties are called “inherited”:

    ```js
    // If we have a method in animal, it can be called on rabbit:
    let animal = {
      eats: true,
      walk() {
        alert("Animal walk");
      }
    };

    let rabbit = {
      jumps: true,
      __proto__: animal
    };

    rabbit.walk(); // Animal walk is taken from the prototype
    ```
* You can have as many prototypes as you want, and you can chain them: if duck inheritis from rabbit inherits from animal, then duck can also inherit from animal.
* For-in loop
  *   If `rabbit` inherits from `animal`, a call to Object.keys(rabbit) will only return the keys of `rabbit`. But, if you use a for-in loop, it iterates over it's own and inherited keys:

      ```js
      let animal = {
        eats: true
      };

      let rabbit = {
        jumps: true,
        __proto__: animal
      };

      // Object.keys only returns own keys
      alert(Object.keys(rabbit)); // jumps

      // for..in loops over both own and inherited keys
      for(let prop in rabbit) alert(prop); // jumps,  eats

      // obj.hasOwnProperty(key) returns boolean if the key at hand (use for-loop) is the object's (true) or inherited (false).
      ```

### Prototype methods, objects without `__proto__`

* The `__proto__` is considered outdated; the modern methods are:
  * _`Object.create(proto, [descriptors])`_ – creates an empty object with given `proto` as `[[Prototype]]` and optional property descriptors.
  * _`Object.getPrototypeOf(obj)`_ – returns the `[[Prototype]]` of `obj`.
  *   _`Object.setPrototypeOf(obj, proto)`_ – sets the `[[Prototype]]` of `obj` to `proto`

      ```js
      let animal = {	eats: true	};

      // create a new object with animal as a prototype
      let rabbit = Object.create(animal);

      alert(rabbit.eats); // true

      // returns the animal (rabbit's prototype)
      alert(Object.getPrototypeOf(rabbit) === animal); // true

      // changes the prototype of rabbit to {}
      Object.setPrototypeOf(rabbit, {});
      ```
*   Object.create's optional second argument:

    ```js
    // We can provide extra properties to the new object there:
    let animal = {	eats: true	};

    let rabbit = Object.create(animal, {
      jumps: {
        value: true
      }
    });

    alert(rabbit.jumps); // true

    // This 2nd argument also allows for better cloning than for-in:
    let clone = Object.create(Object.getPrototypeOf(obj), Object.getOwnPropertyDescriptors(obj));
    // This call makes a truly exact copy of obj, including all properties: enumerable & non-enumerable, data properties and setters/getters – everything, and with the right [[Prototype]].
    ```
* Other Methods:
  * `Object.keys(obj)`, `Object.values(obj)`, `Object.entries(obj)` returns an array of property names/values/key-value pairs.
  * `Object.getOwnPropertySymbols(obj)` - returns an array of all keys with Symbols.
  * `Object.getOwnPropertyNames(obj)` - returns an array of all own string keys.
  * `Reflect.ownKeys(obj)` - returns an array of all keys (basically same as ^).
  * `obj.hasOwnProperty('keyName')` - returns boolean if obj has own (not inherited) key named keyName.

***

## F.PROTOTYPE

* Remember, new objects can be created with a constructor function like `new F()`. So if `F.prototype` is an object, then the `new` operator uses it to set `[[Prototype]]` for the new object.
*   `F.prototype` here is a regular property on `F`. Ie:

    ```js
    let animal = {eats: true};

    function Rabbit(name) {
        this.name = name;
    }

    Rabbit.prototype = animal;	// When a 'new Rabbit' is created, its prototype will be 'animal'
    let rabbit = new Rabbit("Bugs Bunny");

    alert( rabbit.eats );	// true
    ```

***

## NATIVE PROTOTYPES

* All built-in objects follow the same pattern:
  * The methods are stored in the prototype (Array.prototype, Object.prototype, etc...)
  * The object itself stores only the data (array items, object properties, etc...)

***

## CLASSES

* We often need to create many objects of the same kind (ie. users).
* A class is kind of like template code for creating objects, providing initial values for variables and methods.
*   General Syntax:

    ```js
    class className {
        // class methods
        constructor() {...}
        method1() {...}
        method2() {...}
        ...
    }
        
    // CREATE NEW OBJECTS
    let obj1 = new className();		// the constructor() is called by 'new'
    user.method1();
    ```
* In JS, a `class` is a a function (typeof myClass >>> function). After `new className` object is created, when we call its method, it’s taken from the prototype.

### Class Expression

*   Just like functions, classes can be defined inside another expression, passed around, returned, assigned, etc:

    ```js
    let User = class {
      sayHi() {
        alert("Hello");
      }
    };

    // Similar to NFE, class expressions may have a name, call it NCE:
    let User = class MyClass {
      sayHi() { alert(MyClass); } //MyClass name only visible in the class
    };

    new User().sayHi(); // works, shows MyClass definition
    alert(MyClass); // error, MyClass name isn't visible outside of class
    ```

### Getters/Setters

*   Just like literal objects, classes may include getters/setters:

    ```js
    class User {

      constructor(name) {	// invokes the setter
        this.name = name;
      }

      get name() {
        return this.name;
      }

      set name(value) {
        if (value.length < 4) {
          alert("Name is too short.");
          return;
        }
        this._name = value;
      }

    }

    let user = new User("John");
    alert(user.name); // John

    user = new User(""); // Name is too short.
    ```

_**CLASS INHERITANCE**_ - way for one class to extend another class.

### Extends

*   To extend a child class to a parent, `class Child extends Parent`:

    ```js
    // Animal class not shown but Rabbit objects can access Rabbit + Animal methods.
    class Rabbit extends Animal {
        ...
    }
    ```

### Overriding methods

* If both Parent and Child classes share a method name, a call from a Child class object will call the Child class method.

### "Super"

* If you want to intentionally call the Parent method instead of overriding, then call `super.methodName()`. However, arrow functions don't have a `super` keyword.

### Overriding Constructors

* A call to `super(...)` will call the Parent constructor (only from inside the child constructor).
*   If a Child extends a Parent and has no `constructor`, then it calls the Parent constructor passing it all the arguments.

    ```js
    class Animal {
        constructor(name, speed) {
            this.name = name;
            this.speed = speed;
        }
    }

    class Rabbit extends Animal {
        // if you even remove this constructor and leave Rabbit empty, this code will still work
        // because it will just pass the arguments to the Animal constructor.
        constructor(name, speed) {
            super(name, speed);
        }
    }

    let rabbit = new Rabbit("Bugs Bunny", 25);
    console.log(rabbit.name);	// "Bugs Bunny"
    console.log(rabbit.speed);	// 25
    ```
* NOTE: You can override both methods, but also class fields (methods+variables).

***

## STATIC PROPERTIES AND METHODS

* #### Static Methods
  *   Static methods are the same as they're in Java (don't need to make an object to call it):

      ```js
      class User {
        static staticMethod() {
            console.log('hi');
        }
      }

      User.staticMethod(); // hi 
      ```
  * Usually, static methods are used to implement functions that belong to the class, but not to any particular object of it. Call it via: `className.staticMethodName();`
* #### Static Properties
  *   Static properties look like regular class properties but have `static` prepended

      ```js
      class Article {
        	static publisher = "Messi";
      }

      console.log( Article.publisher ); // Messi
      ```
* **Static properties and methods are inherited**

***

## PRIVATE+PROTECTED PROPERTIES AND METHODS

* properties and methods are split into two groups:
  * _**Internal interface**_ – methods+properties, accessible from other methods of the class, but not from the outside.
  * _**External interface**_ – methods+properties, accessible also from outside the class
* Public vs. Private Fields (properties+methods):
  * _**Public**_: accessible from anywhere. They comprise the external interface.
  * _**Private**_: accessible only from inside the class. These are for the internal interface.
    * `#` prefix ie. #name or #returnName(){...}
  * _**Protected**_: like _private_, but child classes can access. These fields will be **read-only**. JS doesn't have an actual implementation but you can emulate it by a class having a getter but not a setter.
    * `_` prefix ie. \_name or \_returnName(){...}

Ie. a Name Class:

```javascript
class NameGenerator {
    _name;		// _ indicates protected
  	#race;		// # indicates private
  
    constructor(name) { this._name = name; }
  	get name() { return this._name; }	// only getter, no setter
}

let nameGenerator = new NameGenerator("John");
console.log(`My name is ${nameGenerator.name}`); // My name is John
nameGenerator.name = "Jane"; // Error; 'name' is read-only
```

***

## EXTENDING BUILT-IN CLASSES

*   You can extend a given class onto built-in classes, like Array/Map, and add functionality:

    Ie. extend a custom PowerArray class to the built-in Array class:

    ```js
    // add one more method to it (can do more)
    class PowerArray extends Array {
      isEmpty() {
        return this.length === 0;
      }
    }

    let arr = new PowerArray(1, 2, 5, 10, 50);
    alert(arr.isEmpty()); // false

    let filteredArr = arr.filter(item => item >= 10);
    alert(filteredArr); // 10, 50
    alert(filteredArr.isEmpty()); // false
    ```

***

## CLASS CHECKING: "instanceof"

*   The `instanceof` operator allows to check whether an object belongs to a certain class. It also takes inheritance into account. The syntax is:

    ```js
    obj instanceof Class
    // returns true if obj is a Class object, or it inherits from Class.

    // ie:
    class Rabbit {}
    let rabbit = new Rabbit();
    alert( rabbit instanceof Rabbit ); // true
    ```
*   It also works with constructor functions:

    ```js
    function Rabbit() {}
    alert( new Rabbit() instanceof Rabbit ); // true
    ```

#### Object.prototype.toString

* We can use `toString` as an extended `typeof` and an alternative for `instanceof`. It will return:
  * For a _number_, it will be `[object Number]`
  * For a _boolean_, it will be `[object Boolean]`
  * For _`null`_: `[object Null]`
  * For _`undefined`_: `[object Undefined]`
  * For _arrays_: `[object Array]`
  * …etc (customizable).

```js
let arr = [];
console.log( Object.prototype.toString(arr) ); // [object Array]
```

***

## MIXINS

* In JS we can only inherit from a single object & a class can only extend one other class.
* A _**mixin**_ is a class containing methods that can be used by other classes without a need to inherit from it.
* The simplest way to implement a _**mixin**_ in JS is to make an object with useful methods, so that we can easily merge them into a prototype of any class.

ie. here the mixin `sayHiMixin` is used to add some “speech” for `User`:

```js
// mixin object
let sayHiMixin = {
  sayHi() { alert(`Hello ${this.name}`); },
  sayBye() { alert(`Bye ${this.name}`); }
};

// usage:
class User {
  constructor(name) { this.name = name; }
}

Object.assign(User.prototype, sayHiBye);	// User now has sayHiBye methods
let me = new User("dev");
me.sayHi();	// Hi dev

// There’s no inheritance, but a simple method copying
```

***

## ERROR HANDLING

*   The try-catch syntax is same as in Java:

    ```js
    try {

      alert('Start of try runs');  // runs 

      lalala; // ERROR

      alert('End of try (never reached)');  // skipped over

    } catch (err) {
      alert(`Error has occurred!`); 	// runs if there's an error.
    }
    ```

#### Error Object

*   When an error occurs, JS generates an object containing the details about it. The object is then passed as an argument to `catch`:

    ```js
    try {
      // ...
    } catch (err) { // <-- "error object", could use another word instead of err
      // ...
    }
    ```
* the error object has two main properties:
  * `name` - Error name. For instance, for an undefined variable that’s `"ReferenceError"`.
  * `message` - Textual message about error details.
*   There are other non-standard properties available in most environments. One of most widely used and supported is:

    * `stack` - Current call stack: a string with info about the sequence of nested calls that led to the error.

    ie:

    ```js
    try {
      lalala; // ERROR
    } catch (err) {
      alert(err.name); 		// ReferenceError
      alert(err.message); // lalala is not defined
      alert(err.stack); // ReferenceError: lalala is not defined at (call stack)

      // Can also show an error as whole. The error is converted to string as "name: message"
      alert(err); // ReferenceError: lalala is not defined
    }
    ```

#### Throwing our own errors

*   Let's say we have a JSON and we are parsing it. What if the `json` is syntactically correct, but doesn’t have a required `name` property?

    ```js
    // Here JSON.parse runs normally, but non-existent 'name' is errorful.
    let json = '{ "age": 30 }';

    try {
      let user = JSON.parse(json);
      alert( user.name ); // ERROR: JSON doesn't have 'name' property
      
    } catch (err) {
      alert( "doesn't execute" );
    }
    ```

#### 'Throw' operator

*   The `throw` operator generates an error. The syntax is:

    ```js
    throw <error object>
    ```
*   JS has many built-in constructors for standard errors: `Error`, `SyntaxError`, `ReferenceError`, `TypeError`, etc... We can use them to create error objects:

    ```js
    let error = new Error(message);
    let error = new SyntaxError(message);
    let error = new ReferenceError(message);
    // For built-in errors (above), the 'name' property is the name of the constructor. And 'message' is taken from the argument.
    ```

    Implementation of try-catch and throw operator:

    ```js
    // Have the abscence of `name` is an error
    let json = '{ "age": 30 }'; // JSON

    try {

      let user = JSON.parse(json); // <-- no errors

      if (!user.name) {	// if 'name' property doesn't exist
        throw new SyntaxError("Incomplete data: no name"); // (*)
      }

      alert( user.name );

    } catch (err) {
      alert( "JSON Error: " + err.message ); // error mesaage display
    }
    ```

    Try-Catch-Finally

    ```js
    try {
       // try to execute the code
    } catch (err) {
       // handle errors
    } finally {
       // execute always
    }
    ```

***

## CALLBACKS

* A callback is a function that's passed into another function and is to be executed after another function has finished executing.

### Function Sequence

*   JS functions are executed in the sequence they are called. Not in the sequence they are defined. ie:

    ```js
    // myDisplayer changes innerHTML of an element, so the final call to it will be the final product.
    function myFirst() { myDisplayer("Hi"); }
    function mySecond() { myDisplayer("Bye"); }

    myFirst();
    mySecond();
    // this example ends up displaying "Bye"
    ```

### Callback Function

*   Let’s add a `callback` function as a second argument (usually anonymous) to `loadScript` that should execute when the script loads.

    ```js
    function myDisplayer(some) {
    	document.getElementById("demo").innerHTML = some;
    }

    function myCalculator(num1, num2, myCallback) {
        let sum = num1 + num2;
        myCallback(sum);
    }

    myCalculator(5, 5, myDisplayer);
    ```
* Using a callback, you can call `myCalculator` with a callback, and let the calculator function run the callback after the calculation is finished.
  * Right: myCalculator(5, 5, myDisplayer);
  * Wrong: myCalculator(5, 5, myDisplayer());

### Callback in Callback

*   ie. We can load two scripts sequentially: the first one, and then the second one after it, by putting the second callback call inside the first callback:

    ```js
    // After the outer loadScript is complete, the callback initiates the inner one.

    loadScript('/my/script.js', function(script) {
        alert(`Cool, the ${script.src} is loaded, let's load one more`);

        loadScript('/my/script2.js', function(script) {
        	alert(`Cool, the second script is loaded`);
        });
    });
    ```

### Callback Error handling

*   ie. In the case the script loading fails, the callback need to react to the error. The error handling usage:

    ```js
    loadScript('/my/script.js', function(error, script) {
        if (error) {
        	// handle error
        } else {
        	// script loaded successfully
        }
    });
    ```
* The first argument of the callback is actually reserved for an error if it occurs.

***

## PROMISES

* "Producing code" - code that does something and takes time. ie. code that loads the data over a network
* "Consuming code" - code that wants the result of the “producing code” once it’s ready. ie. Functions
* A Promise - a JavaScript object that links producing code and consuming code

### Constructor Syntax

```js
let promise = new Promise(function(resolve, reject) {
	// executor (the producing code)
});
```

* _**`executor`**_ - function passed to `new Promise`. "Producing Code"
* _**`resolve`/`reject`**_ - callbacks provided by JS itself. When the executor obtains the result, it should call one of these callbacks:
  * _**`resolve(value)`**_ — if the job is finished successfully, with result `value`.
  * _**`reject(error)`**_ — if an error has occurred, `error` is the error object.
* The `promise` object returned by the `new Promise` constructor has these internal properties:
  * `state`
    * initially `"pending"`, then changes to either
    * `"fulfilled"` when `resolve` is called or
    * `"rejected"` when `reject` is called.
  * `result`
    * initially `undefined`, then changes to either
    * `value` when `resolve(value)` is called or
    * `error` when `reject(error)` is called.

ie:

```js
let myPromise = new Promise(function(resolve, reject) {
    // after 1 second signal that the job is done with the result "done"
    // calling resolve('done') changes myPromise properties to (state='fulfilled' and result='done')
    setTimeout(() => resolve("done"), 1000);
});

let promise = new Promise(function(resolve, reject) {
    // after 1 second signal that the job is finished with an error
	// calling reject(error) changes myPromise properties to (state='rejected' and result=error)
    setTimeout(() => reject(new Error("Whoops!")), 1000);
});
```

* Note: there can only be one call to resolve/reject in the executor. All other resolve/reject calls below the first one are ignored.

### Consumers: then, catch, finally

*   The _**state**_ and _**result**_ properties of the Promise object are _**internal**_. We can’t directly access them. We have to use the methods `.then`/`.catch`/`.finally`

    **then**

    ```js
    // general syntax
    myPromise.then(
      function(result) { /* handle a successful result */ },
      function(error) { /* handle an error */ }
    );
    ```

    * The 1st argument of `.then` is a function that runs when the promise is _**resolved**_, and receives the result
    * The 2nd argument of `.then` is a function that runs when the promise is _**rejected**_, and receives the error

    ie.

    ```js
    let myPromise = new Promise(function(resolve, reject) {
      setTimeout(() => resolve("done!"), 1000);
    });

    // a callback to resolve from the executor runs the first function in .then
    myPromise.then(
        result => alert(result), // shows "done!" after 1 second
        error => alert(error) // doesn't run
    );
    ```

    **catch**

    *   If we’re interested only in errors, then we can use `null` as the first argument:

        ​ `.then(null, errorHandlingFunction)`
    *   Or we can use `.catch(errorHandlingFunction)`, which is exactly the same:

        ```js
        let myPromise = new Promise((resolve, reject) => {
            setTimeout(() => reject(new Error("Whoops!")), 1000);
        });

        // .catch(f) is the same as promise.then(null, f)
        myPromise.catch(alert); // shows "Error: Whoops!" after 1 second
        ```

    **finally**

    * Just like there’s a `finally` clause in a try-catch there’s `finally` in promises.
    * The call `.finally(f)` is similar to `.then(f, f)` in the sense that `f` always runs when the promise is settled: be it resolve or reject.
    *   It's a good handler for performing cleanup ie. stopping our loading indicators (not needed anymore regardless of outcome)

        ```js
        // here, there’s an error in the promise, passed through finally to catch:
        let myPromise = new Promise((resolve, reject) => {
            throw new Error("error");
        })

        myPromise.finally(() => alert("Promise ready"))
        myPromise.catch(err => alert(err));  // <-- .catch handles the error object
        ```

        ie:

        ```js
        function loadScript(src) {
            return new Promise(function(resolve, reject) {
                let script = document.createElement('script');
                script.src = src;

                script.onload = () => resolve(script);
                script.onerror = () => reject(new Error(`Script load error for ${src}`));

                document.head.append(script);
            });
        }

        // loadscript returns a promise object
        let myPromise =loadScript("/myscript.js");

        myPromise.then(
            script => alert(`${script.src} is loaded!`),
            error => alert(`Error: ${error.message}`)
        );

        promise.then(script => alert('Another handler...'));
        ```

### Promise Chaining

```js
new Promise(function(resolve, reject) {

  setTimeout(() => resolve(1), 1000); // (*)

}).then(function(result) { // (**)

  alert(result); // 1
  return result * 2;

}).then(function(result) { // (***)

  alert(result); // 2
  return result * 2;

}).then(function(result) {

  alert(result); // 4
  return result * 2;

});
```

Here the flow is:

1. The initial promise resolves in 1 second `(*)`,
2. Then the `.then` handler is called `(**)`.
3. The value that it returns is passed to the next `.then` handler `(***)`
4. …and so on.
