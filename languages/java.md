# Java

`Skipped: Recursion`

#### **`Lecture Notes`**

_Source Code_: '.java' files you write _source code_ in.

Java is a statically-typed language (must assign type to variable in declaration; variables can't switch types)

_Portable 'byte' Code_: the compiler (javac) generates byte code in a ‘.class’ file which can be run on any Java Virtual Machine (JVM). JVM efficiently interprets\* byte code in the .class file into native machine code (binary) and executes it.

The Java Platform consists of 2 parts:

1. JVM
2. Java API (huge library of handy software packages that programmers can use)

When running Java Programs:

* `javac filename.java` = compile code.
  * The compiler (javac) generates the '.class' file which contains instructions for the JVM.
  * '.class' files contain 'byte code' which you can't edit
* `java filename.java` = execute code

Create 1 Folder per program as to organize and group the .class files to their corresponding .java files.

In Java, every statement must end in a semicolon.

**Integer Division and Remainder**

* When integers divide into each other, the result is an integer.
*   Integer division loses all fractional parts of the result and does not round.

    ```java
    int result = 7 / 4; // 1 from 1.75
    ```

```java
n % 2    // if (n is even) gives 0, else 1 (or -1 if n < 0)

n % 10    // gives the last digit of n (rightmost)
n % 100    // gives the last 2 digits of n (from right)

n / 10  // gives n without the last digit (n is int)
n / 100 // gives n without the last 2 digits (n is int)
```

***

#### The Main Method

* The `main()` method is required and you will see it in every Java program. Any code inside the `main()` method will be executed.
*   Remember that _**every Java program has a `class` name which must match the filename**_, and that every program must contain the `main()` method.

    ```java
    public class Main {
      public static void main(String[] args) {
        System.out.println("Hello World");
      }
    }
    ```

***

#### Comments

Single-line: `// comment`

Multi-line: `/* comment */`

***

### Formatting with printf()

neat shortcut in printing instead of print() and println()

### Syntax

```java
System.out.printf(format, arguments);   
           [format] -  text marked up with % formatters
        [arguments] - variables separated by commas corresponding to the occurences of the % formatters
```

​ Formatters: ​ %d - int ​ %f - double ​ %.2f - 2 decimals places after period (3.141592653589 -> 3.14) ​ %c - char ​ %s - string ​ %b - boolean ​ %n - newline

​

```java
// ex.
System.out.printf("%d %f %c %s %b %n", int, double, char, string, boolean);
System.out.printf("Hello %s!%n", "World");

//  %s is replaced by the first argument (the only one): "World". Then follows %n which is a new line.
```

***

#### Variables

Variables are containers for storing data values, and there are different **types** of variables:

```java
int num = 5;
String text = "Hello";
float num2 = 5.99; 
char letter = 'x';
boolean isRaining = true;
```

**Variable Declaration**

*   declaring a variable means specifying a `variable name` and its `data type`.

    ```java
    int age; // declare

    // you can declare many at once if they're the same type:
    int x = 1, y = 2, z = 3;
    ```

**Variable Initialization**

*   initializing a variable means assigning a value to the variable.

    ```java
    int age; // declare
    age = 18; // init

    int price = 99; // declare and init at once
    ```

(Note that if you assign a new value to an existing variable, it will overwrite the previous value.)

**`Final` Variable Types**

* When a variable is defined with the reserved word `final`, its value can never be changed.
*   It is customary (not required) to use all UPPER\_CASE letters for constants (easy to pick out constants in the code)

    ```java
    final int NUMBER = 15;
    NUMBER = 20; // error
    ```

#### Variable Scope

* _**Local Scope**_ - variables declared and only existing inside methods ie. formal parameter variables.
* _**Block Scope**_ - variables decalred and only existing within their parent { }'s.
* _**Global Scope**_ - variables which can be used and changed by code anywhere.

General rules for variable naming:

* can contain letters, digits, underscores, and dollar signs
* must begin with a letter
* snakeCase
* can also begin with $ and \_
* are case sensitive
* Reserved words cannot be used as names

***

#### Data Types

* Data types are divided into two groups:

1. _**`Primitive data types`**_
   * specifies the size & type of variable values, and has no additional methods.
   * `int`
     * whole numbers between -2,147,483,647 (Integer.MIN\_VALUE) and +2,147,483,647 (Integer.MAX\_VALUE). Use long/short outside this range.
     * Whole number
   * `float`
     * The single-precision floating-point type with about 7 decimal digits and a range of about +/- 1e38.
   * `double`
     * The double-precision floating-point type, with about 15 decimal digits and a range of about +/- 1e308.
   * `short`
     * The short integer type with range -32,768 ... +32767.
     * Whole number
   * `long`
     * The long integer type with about 19 decimal digits.
     * Whole number
   * `byte`
     * The type describing a byte consisting of 8 bits, with range -128 ... 127
     * Whole number
   * `char`
     * The character type representing code units in Unicode
     * Characters (no math)
   * `boolean`
     * True or False
2. _**`Reference data types`**_
   * are called **reference types** because they refer to objects.
   * `Class`, `object`, `array`, `string`, and `interface`

The main differences between the two:

* Primitive types are predefined in Java. Non-primitive types are created by the programmer and is not defined by Java (except for `String`).
* Non-primitive types can be used to call methods to perform certain operations, while primitive types cannot.
* A primitive type has always a value, while non-primitive types can be `null`.
* A primitive type starts with a lowercase letter, while non-primitive types starts with an uppercase letter.
* The size of a primitive type depends on the data type, while non-primitive types have all the same size.

_**Note:**_

* **Strings use "" and chars use ''**
* **Max and Min value for an int is +2,147,483,647 and -2,147,483,647, respectively** (for any values above max or below min, use the _long_ , _short_, or _double_ data type). This value is found in `Integer.MAX_VALUE` and `Integer.MIN_VALUE`.
*

**Number Literals**

*   Sometimes when you just type a number in an expression, the compiler has to ‘guess’what type it is:

    ```java
    int a=6, b=-6, c=0; // whole numbers above, below, or 0, are integers
    double a=0.5, b=1.0, c=1E6, d=-6.4E24 // decimal and exp. notation are double
    ```

***

#### Type-Casting

**Variable Conversion:**

```java
// Double -> Int
int a = (int) double_val;
// ditches the fractional part of floating point value

// String -> Int
Integer.valueOf(string)

// Int -> String
Integer.toString(int)

// Int/String -> Double
Double.valueOf(string)
Double.valueOf(int)

// Char/Double/Boolean -> String
String.valueOf(double)
String.valueOf(char)
String.valueOf(boolean)

// String -> Boolean
Boolean.valueOf(string)
```

**Ex.**

```java
// Ex. 
String valueAsString = "42";
int value = Integer.valueOf(valueAsString);
System.out.println(value); // 42, but as int
```

***

#### Operators

_**Arithmetic Operators**_: `+`, `-`, `*`, `/`, `%`, `++`, `--`

*   Note: comparison operators have lower precedence than arithmetic operators so:

    ```java
    if (a > b + 1) // evals. b + 1 then compares with a
    if (3 == 5 - 2) // evals. 5 - 2 then compares with 3 (true)
    ```

_**Assignment Operators**_

| Operator | Example | Same As    |
| -------- | ------- | ---------- |
| =        | x = 5   | x = 5      |
| +=       | x += 3  | x = x + 3  |
| -=       | x -= 3  | x = x - 3  |
| \*=      | x \*= 3 | x = x \* 3 |
| /=       | x /= 3  | x = x / 3  |
| %=       | x %= 3  | x = x % 3  |
| &=       | x &= 3  | x = x & 3  |
| \|=      | x \|= 3 | x = x \| 3 |
| ^=       | x ^= 3  | x = x ^ 3  |
| >>=      | x >>= 3 | x = x >> 3 |
| <<=      | x <<= 3 | x = x << 3 |

_**Comparison Operators**_: `==`, `!=`, `>`, `>=`,`<`, `<=`

* most of these comparison operators ( >, <, >=, and <=) can be applied only to _primitives_. Two (== , !=) can be used for _any object_ but when applied to _reference types_, they test if they _point to same object_ rather than _have same value_.

_**Logical Operators**_: `&&`, `||`, `!`

***

## Methods

**Creating and Calling Methods**

```
// A method must be declared within a class. It is defined with the name of the method, followed by ()'s.

public static void sayHi() {
    System.out.println("hello");
}

//to call this method:
sayHi();
```

**Method Parameters**

* _**Formal Parameters**_: parameters in function signature
* _**Actual Parameters**_: actual values passed to function call

```
// Information can be passed to methods as parameter. Parameters act as variables inside the method.

public class MyClass {
      public static void sayHi(int age) {
            System.out.println("Hello, " + age);
      }

      // main block
      public static void main(String[] args) {
            sayHi("Rachel");           // "Hello Rachel"
       }
}
```

#### Return

* Code underneath a `return` call is unreachable code.
* The type of the value returned must match the return-type specified in a method's signature.
* A method can use multiple `return` statements.
* Methods are not required to return a value. In this case, the return-type in the method signature should be `void`

```
// returns a value to the function call

public class MyClass {
      public static int addFive(int x) {
          return 5 + x;
      }

      public static void main(String[] args) {
            System.out.println(addFive(3));     // addFive(3) --> 8
      }
}
```

#### Method Overloading

*   multiple methods can have the _**same name**_ with _**different parameters**_. It will call the function whose actual parameters match the formal parameters types and positions in the function call.

    ```java
    static int plusMethod(int x, int y) {
          return x + y;
    }

    static double plusMethod(double x, double y) {
          return x + y;
    }

    public static void main(String[] args) {
        int myNum1 = plusMethod(8, 5);                    // calls int method (of same name)
        double myNum2 = plusMethod(4.3, 6.26);  // calls double method (of same name)
    }
    ```

**Method Comments**

*   To write a Javadoc comment above each method:

    * /\*\*
      * Note the purpose of the method
      * @param - describe each parameter variable
      * @return - describe the return value
    * \*/

    ```java
    /**
        Computes the volume of a cube.
        @param sideLength the side length of the cube
        @return the volume
    */
    public static double cubeVolume(double sideLength) {...}
    ```

***

## String Methods

**`toLowerCase()` - converts a string to lower case letters.**

```
txt.toLowerCase()
```

**`toUpperCase()` - converts a string to upper case letters.**

```
txt.toUpperCase()
```

**`length()` - returns int value of the number of characters in string. The length of an empty string is 0**

```
String txt = "hello";
int x = txt.length(); //5
```

**`contains()`- finds out if a string contains a sequence of chars. Returns true if the chars exist; false if not.**

```
String myStr = "Hello";
myStr.contains("Hel");   // true
myStr.contains("e");     // true
myStr.contains("Hi");    // false
```

**`equals()` - compares two strings, and returns true if the strings are equal, and false if not.**

**`equalsIgnoreCase()` - compare strings to find out if they are equal AND IGNORE CASE DIFFERENCES**

* Don't compare strings using the == operator since it will check if the two Strings point to the same object since Strings are reference types.

```
String myStr1 = "Hello";
String myStr2 = "Hello";
String myStr3 = "Another String";
myStr1.equals(myStr2); // Returns true because they are equal
myStr1.equals(myStr3); // false
```

**`compareTo()`, `compareToIgnoreCase()` - returns An int value:**

* 0 if the string is equal to the other string.
* < 0 if the string is lexicographically less than the other string.
*   \> 0 if the string is lexicographically greater than the other string (more characters).

    ```
    String myStr1 = "Hello";
    String myStr2 = "Hello";
    myStr1.compareTo(myStr2); // Returns 0 because they are equal
    ```

**`indexOf()` - returns the index of the first occurrence of specified char(s) in a string**

**`lastIndexOf()` - returns the index of the last occurrence of specified char(s) in a string**

```
String myStr = "Hello planet earth, you are a great planet.";
myStr.IndexOf("planet");  // 6
myStr.lastIndexOf("planet");  //36
```

**`concat()`- appends/concatenates a string to the end of another string**

```
String firstName = "Barry ";
String lastName = "Allen";
firstName.concat(lastName); //Barry Allen
```

**`replace()` - searches string for specified char(s), and returns new string where specified char(s) are replaced**

```
String myStr = "Hello";
myStr.replace('l', 'p');  //replace(searchFor, ReplaceWith)
// returns "heppo"
```

**`trim()` - removes whitespace from both ends of a string. This method does not change the original string**

```
String myStr = "       Hello World!       ";
myStr.trim(); // "Hello World!"
```

**`startsWith()` - checks whether a string starts with the specified char(s).**

**`endsWith()` - checks whether a string ends with the specified char(s).**

```
String myStr = "Hello";
System.out.println(myStr.startsWith("Hel"));   // true
System.out.println(myStr.startsWith("llo"));   // false
System.out.println(myStr.endsWith("o"));     // true
```

**`charAt()` - returns the char at the specified index in a string**

```
String myStr = "Hello";
char result = myStr.charAt(0);  //'H'
```

**`split()` - splits a string at a specified char and creates an array; parameter is what's being removed.**

If you split a string and an int, they both become strings so convert using Integer.valueOf()

```
String text = "first second third fourth";
String[] pieces = text.split(" ");    //["first", "second", "third", "fourth"]
```

**`subString()` - returns a substring of this string; from the first index to the second (exclusive); otherwise extends to the end of this string**

```
String str = "Hello world!";
str.substring(0, 5);     //"Hello"
str.substring(6);        //"world!"
```

**`copyValueOf()` - returns a String that contains the characters of the character array**

```
char[] Str1 = {'h', 'e', 'l', 'l', 'o', ' ', 'w', 'o', 'r', 'l', 'd'};
String Str2 = "";
Str2 = Str2.copyValueOf( Str1, 0, 7 );  //str2 = "hello w"

//copyValue(char[], int offset, int end)    where offset is the index to start and end is the end
```

***

## Math Methods `import java.lang.Math;`

**`xxxValue()` - returns the primitive data type that is given in the signature.**

```
int x = 5;

x.byteValue();
x.doubleValue();
x.longValue();
x.shortValue();
x.floatValue();
```

**`parseXXX()` - used to get the primitive data type of a certain String.**

```
int x = Integer.parseInt("9");                // x = 9
double c = Double.parseDouble("444");      // c = 444
```

**`abs()` - gives the absolute value of the argument.**

```
int a = -8;
double d = -8.5;

Math.abs(a);  // 8
Math.abs(d);  // 8.5
```

**`ceil()` - returns the smallest integer that is greater than or equal to the argument.**

```
double d = 4.3;
double x = -100.678;   

Math.ceil(d);   // 5.0
Math.ceil(f);   // -100.0
```

**`floor()` - returns the largest integer that is less than or equal to the argument.**

```
double d = 4.3;
float f = -100.678; 

Math.floor(d);   // 4.0
Math.ceil(f);    // -101.0
```

**`rint()` returns the integer (double.0) that is closest in value to the argument. Parameter must be double**

```
double d = 100.675;
double e = 100.500;
double f = 100.200;

Math.rint(d);   //101.0
Math.rint(e);   //100.0
Math.rint(f);   //100.0
```

**`round()` - returns the closest long or int to the argument. Parameter must be double or float**

```
double d = 100.675;
double e = 100.500;
float f = 100;

Math.round(d);   //101
Math.round(e);   //101
Math.round(f);   //100
```

**`min()` - gives the smaller of the two arguments**

```
Math.min(5, 10);            //returns 5
Math.min(12.123, 12.456);   //returns 12.123
```

**`max()` - gives the larger of the two arguments**

```
Math.max(5, 10);            //returns 10
Math.max(12.123, 12.456);   //returns 12.456
```

**`pow()` - returns the value of the first argument raised to the power of the second argument.**

```
Math.pow(12, 2);   //144
```

**`sqrt()` - returns the square root of the argument.**

```
Math.sqrt(144);   //12
```

**`cbrt()` - returns the cube root of the argument.**

```
Math.cbrt(125);   //5.0
```

**`Math.PI` - returns the value of pi to the 15th decimal.**

```
double area = Math.PI * (radius * radius);    //Math.PI acts as 3.14... itself
```

**`random()` used to generate a random number between 0.0 and 1.0**

```
// 100 is the ending value. 1 is the starting value. Inclusive
Math.floor( Math.random() * 100 ) + 1;

// 1-6 inclusive
int dieRoll = (int)( Math.random() * 6 ) + 1; 
```

***

## Conditionals

**`If`**

```
if (EpxressionTrue) {
    System.out.println("do this");
}
```

**`If-Else`**

```
if (EpxressionTrue) {
    System.out.println("do this");
} else {
    System.out.println("or else do this");
}
```

**`Else-If`**

```
if (EpxressionTrue) {
    System.out.println("do this");

} else if (additional condition){
    System.out.println("or else do this");

} else {
    System.out.println("or else do this");
}
```

**`For`**

```
for (int i = 0; i <= 10; i++) {
    System.out.println(i);
}
// counts up to 10.
// initializes i, checks expression, increments i.
```

**`For-Each` (arrays)**

```
// Initialize "var", the variable used to store each Integer in list as it iterates.
for (type var : array) 
{ 
    //code
}

// ex. find the sum of numbers in list
for(int val: listOfNumbers) {
  sum += val;
}
```

**`While`**

```
// a while loop will keep on running the code inside until the argument is false.
int i=0;
while(i < 5) {
    System.out.println(i);
    i++;
}
// Make sure you have an exit card (break;) for the while loop or else you'll end up with an infinite loop
```

**`Do-While`**

```
// do-while will run code then check expression whereas while-loops need the expression to be true to enter.
do{
    System.out.println(i);
    i++;
} while(i < 5);

// if the expression at the bottom is true, it will jump to the top and work it's way down again.
```

**`Continue` - breaks out of the inner loop and goes to the top of the outer loop.**

```
// While-true loops are handy when the program has to repeat something until the user provides certain input
while (true) {
    System.out.println("Insert positive integers");
    int number = sc.nextInt());

    if (number <= 0) {
        System.out.println("Unfit number! Try again.");
        continue;
    }
    System.out.println("Your input was " + number);
}
```

**`Break` - breaks out of the current loop**

```
for (int i = 0; i < 10; i++) {
      // exits the for-loop when i reaches 4
      if (i == 4) {
            break;
      }
        System.out.println(i);
}
```

**`Switch-Case`**

```
switch(value){
    case x:
        // do something
        break;
    case y:
        // do something
        break;
      case a: case b: 
            // will do this if value is case a OR case b
            // you can stack cases if you want the same action for them
        break;
      default:
        // if value isn't x or y, then it will do the code in default.  
}
```

**`Modulo`**

```
7 % 2

// prints the remainder, 1
// can be used to check if even (x % 2 == 0) or odd (x % 2 != 0)
```

**`Try-Catch`**

```
try{
    //code block
} catch(Exception e) {
    //code block to handle errors
}

/*
tries the code in the try code block. If it throws an exception, it will instead run the catch{}'s code

Replacing the "Exception" and keeping the "e",
        "Exception" can be replaced with:
        - ArithmeticException
        - FileNotFoundException
        - ArrayIndexOutOfBoundsException
        - SecurityException
        - and many more
*/
```

***

### Ternary Operator

**The Java ternary operator functions like a simplified Java if statement.**

* The ternary operator consists of a condition that evaluates to either true or false, plus a value that is returned if the condition is true and another value that is returned if the condition is false.

**Format**

* System.out.println( expression ? "true" : "false");
* System.out.println( expression ? "true" : expression2 ? "false" : "maybe");

**Here are some simple Java ternary operator examples:**

```
System.out.println( (a > b) ? ("A") : (b < a) ? ("B") : ("Tie") );
String name = stringName.equals("uppercase") ? "JOHN" : "john";
```

* ? checks if statement is true; if yes, print what follows the question mark
* : separates the "arguements". If the first one is false, it goes to second argument

***

### Misc

**`Swapping Values;`**

```
int a = 7, b = 10;

a ^= b;
b ^= a;
a ^= b;
// Now, a=10, b=7
```

**`Import Keyword`**

The import keyword is used to import a package, class or interface.

```
// You can import just the classes you need from a package.
// Just provide an import statement for each class that you want to use:

// Import the Scanner class
import java.util.Scanner;

// Another option is to import everything at the same level in a package using import packageName.*.
import java.util.*;

// Below I've provided a list with useful classes to import and their key uses.
```

| class               | highlight                                                                              |
| ------------------- | -------------------------------------------------------------------------------------- |
| java.lang.String    | used to create / operate immutable string literals                                     |
| java.lang.Exception | helps deal with exception and error handling                                           |
| java.util.ArrayList | implementation of array data structure                                                 |
| java.util.HashMap   | implementation of a key-value pair data structure                                      |
| java.lang.Object    | contains early methods like equals, hashcode, clone, toString, etc                     |
| java.util.Date      | used to work with date and current time                                                |
| java.util.Iterator  | allows use of an 'Iterator' object that can be used to loop through Lists and HashSets |

#### Input

* The `Scanner` class allows you to read keyboard inputs from the user.
*   Reading certain variables:

    | int         | sc.nextInt();                        |
    | ----------- | ------------------------------------ |
    | **double**  | **sc.nextDouble();**                 |
    | **String**  | **sc.nextLine();** or **sc.next();** |
    | **char**    | **sc.char().charAt(0);**             |
    | **boolean** | **sc.nextBoolean();**                |

    ```java
    import java.util.Scanner; // import it
    ...
    Scanner sc = new Scanner(System.in); // create Scanner object
    ...
    System.out.print("Enter number: "); // best to avoid println
    int num = sc.nextInt();
    ```

**Escape Sequences**

* allows us to use special characters inside strings as visual components rather than functional ones. Ex. using quotes "" inside a String which has ""s already gives some funky errors.
* Preface the special character with a **\\**
* &#x20;does a newline in a string

**Use of Epsilon**

* Use a very small value to compare the difference if floating-point values are ‘close enough’
*   The magnitude of their difference should be less than some threshold.

    ```java
    final double EPSILON = 1E-14;
    double r = Math.sqrt(2.0);

    if (Math.abs(r * r - 2.0) < EPSILON) {
            System.out.println("Math.sqrt(2.0) squared is ~= 2.0");
    }
    ```

#### Enum

* **Enum** is short for "enumerations", which means "specifically listed".
* Use `enums` when you have values that you know aren't going to change.
* An `enum` is a special "class" that represents a group of **constants**.
* To create an `enum`, use the `enum` keyword and separate the constants with a comma.
*   You can access `enum` constants with _dot notation_

    ```java
    // assume constants hold some values.
    enum Level {
      LOW,
      MEDIUM,
      HIGH
    }

    Level myVar = Level.MEDIUM;
    ```
* **Enum iteration**
  *   The enum type has a `values()` method, which returns an array of all enum constants. This method is useful when you want to loop through the constants of an enum:

      ```java
      for (Level myVar : Level.values()) {
        System.out.println(myVar);
      }
      ```

**Sentinel Values**

* Sentinel values are often used when you don't know how many things you're going to get from input.
* A Sentinel value is simply a value which when picked up by the Scanner, will stop reading the input and do something else.
*   A Sentinel value denotes the end of a data set, but it's not apart of the data!

    ```java
    salary = sc.nextDouble(); // read first input
    // the sentinel value here is -1
    while (salary != -1) {
            sum += salary;
            count++;
            salary = sc.nextDouble();  // read input
    }
    ```
*   But sometimes you might even have -1 in the dataset, so instead you can use a non-numeric sentinel (entering a non-numeric value as input would end the input)

    ```java
    System.out.print("Enter values, Q to quit: ");

    // sc.hasNextDouble() returns boolean
    // true - if all's well
    // false - if not a number
    // [entering a non-numeric value would denote end of dataset]
    while (sc.hasNextDouble()) {
            value = sc.nextDouble();    // read input
          // do something
    }
    ```

**Static Blocks**

*   A block of code which is executed before the main method at the time of classloading.

    ```java
    class Test{  
     static{System.out.println("A");}   // static block prints "A" before main method prints "B"

     public static void main(String args[]){  
                  System.out.println("B");  
     }
    }  
    ```

**Wrapper Classes**

* Java provides wrapper classes for primitive types
*   Conversions are automatic using _**auto-boxing**_:

    ```java
    // Primitive --> Wrapper Class:
    double x = 29.95; 						// primitive (with value)
    Double wrapper;								// wrapper class
    wrapper = x;  								// boxing

    // Wrapper Class --> Primitive:
    double x;											// primitive
    Double wrapper = 29.95;				// wrapper class (with value)
    x = wrapper;  								// unboxing
    ```
* Primitives and their Wrapper-Equals:
  * `byte=Byte`, `boolean=Boolean`, `char=Character`, `double=Double`, `float=Float`, `int=Integer`, `long=Long`, `short=Short`.
* You cannot use primitive types in an _**ArrayList**_, but you can use their wrapper classes

***

## Data Structures

### ¬ Arrays

* Arrays are used to store multiple values in a single variable, instead of declaring separate variables for each value.
* You don't need to import any packages for Arrays (you do though for Arraylists)
* With arrays, the _size cannot be modified_. If you wanted to add or remove elements from an array, you'd have to create a new one.
  * Use an Array if: The size of the array never changes, You have a long list of primitive values (efficiency reasons), Your instructor wants you to.
  * Use an ArrayList if: For just about all other cases, Especially if you have an unknown number of input values.

**`Declaration` - define the variable type with square brackets:**

```
String[] cars;
int[] numbers;
```

**`Initialization` - use an Array literal to insert values; place the values inside curly braces:**

```
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
int[] numbers = {10, 20, 30, 40};


// Initializing an empty array with a specified number of spaces:
int[] anArray = new int[10]
```

**`Printing` - import java.util.Arrays;**

```
int[] numbers = {10, 20, 30, 40};

// Arrays.toString(<array>) returns a string of the array (so you can use string methods on it)
System.out.println(Arrays.toString(numbers));  // [10, 20, 30, 40]
```

**`Accessing Elements` - access an array element by referring to the index number (arrays start at 0)**

* Make sure the index you provided is exists or else you'll get a IndexOutOfBoundsError
* Empty arrays hold `null` values by default

```
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
System.out.println(cars[0]); // volvo
```

**`Changing Array Elements` - to change the value of a specific element, refer to the index number**

* Arrays are mutable

```
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
cars[0] = "Ferrari";

// now, cars = {Ferrari, BMW, Ford, Mazda}
```

**`Array Length` - find out how many elements an array has, use the `.length` property**

```
// Not to be mistaken for 'length()' method which is a string method

String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
System.out.println(cars.length); // 4 (items in cars array)
```

**`Iterating over an Array`**

```
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};

// use .length to specify the loop count
for (int i = 0; i < cars.length; i++) {
    System.out.println(cars[i]);
}
```

**`Iterating using For-Each loop`**

* For-each loops are used exclusively to loop through elements in arrays. This loop goes through the array 1 by 1 and assigns it to the variable.

```
/*
for (type variable : arrayname) {
        // code
}
*/

String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};

for (String i : cars) {
    System.out.println(i);
}
```

Common Array Algorithms:

*   `Sum and Average Values`

    ```java
    double total = 0, average = 0;
    for (int i = 0; i < values.length; i++nt : values)	 total = total + element;
    if (values.length > 0) { average = total / values.length; }
    ```
*   `Find the Maximum or Minimum`

    ```java
    // Max
    double largest = values[0];
    for (double element : values) if element > largest) largest = element;

    // Min
    double smallest = values[0];
    for (double element : values) if element < smallest) smallest = element;
    ```
*   `Linear Search`

    ```java
    int searchedValue = 100;  int pos = 0;
    boolean found = false;
    while (pos < values.length && !found) {
    		if (values[pos] == searchedValue)
          	found = true; 
    		else pos++; 
    }

    if (found) System.out.println(“Found at position: ” + pos); 
    else System.out.println(“Not found”);
    ```
*   `Removing an Element and maintaining order`

    ```java
    for (int i = pos; i < currentSize - 1; i++) {
    		values[i] = values[i + 1];
    }
    currentSize--;
    ```
*   `Inserting an Element and maintaining order`

    ```java
    if (currentSize < values.length) {
    		currentSize++;
    		for (int i = currentSize - 1; i > pos; i--) values[i] = values[i - 1];  // move down
    		values[pos] = newElement;     // fill hole
    }
    ```
*   `Growing an Array`

    ```java
    // Copy the contents of one array to a larger one
    // Change the reference of the original to the larger one

    double[] values = new double[6];
    . . . // Fill array
    double[] newValues = Arrays.copyOf(values, 2 * values.length); // ie. 2x the size of an existing array
    values = newValues;
    ```
*   `Copying Arrays` - Not the same as copying only the reference; Copying creates two set of contents!

    ```java
    double[] values = new double[6];
    . . . // Fill array
    double[] prices = values;   // Only a reference so far
    double[] prices = Arrays.copyOf(values, values.length);
    // copyOf creates the new copy, returns a reference
    ```
* `Reading Input`
  *   Case A: _**Known**_ number of values to expect - Make an array that size and fill it one-by-one

      ```java
      double[] inputs = new double[NUMBER_OF_INPUTS];
      for (i = 0; i < values.length; i++) {
        	inputs[i] = in.nextDouble();
      }
      ```
  *   Case B: _**Unknown**_ number of values - Make maximum sized array, maintain as partially filled array

      ```java
      double[] inputs = new double[MAX_INPUTS];
      int currentSize = 0;
      while (in.hasNextDouble() && currentSize < inputs.length) {
      		inputs[currentSize] = in.nextDouble();
      		currentSize++;
      }
      ```

***

### ¬ 2D Arrays

* You don't need to import any packages for 2D Arrays.
* 2D Arrays have Rows & Columns and is aka ''Matrix'.

**`Declaration`**

* Use two ‘pairs’ of square braces: `<type>[][] <name> = new <type>[#rows][#cols]`
* _**#rows**_ is basically the number of arrays in the the 2d array
*   _**#cols**_ is basically the size of each array in 2d array (given they are all the same size)

    ```java
    final int ROWS = 4, COLS = 3;
    int[][] counts = new int[ROWS][COLS];

    // You can also define a 2d Array as a Literal:
    int[][] counts = {
      { 1, 0, 1 },
      { 1, 1, 0 },
      { 0, 0, 1 },
      { 1, 0, 0 },
    };
    ```

**`Accessing`**

*   Use two index values: `int value = counts[3][1];` gets element at index-3 ROW & index-1 COL.

    ```java
    int[][] counts = {
      { 1, 2, 3 }, // row index-0
      { 4, 5, 6 }, // row index-1
    	{ 7, 8, 9 }, // row index-2
    };

    int one = counts[0][0];
    int five = counts[1][1];
    int nine = counts[2][2];
    ```

**`Iteration`**

*   Use nested for loops where Outer row(i) , inner column(j):

    ```java
    for (int i = 0; i < ROWS; i++) { 									// loop thru ROWS
    		for (int j = 0; j < COLS; j++) {
    				System.out.println( counts[i][j] ); 	// loop thru COLS in ROWS
        }
    }
    ```

**`Locating Neighbouring Elements`**

!\[Screen Shot 2022-01-31 at 1.04.36 PM]\(/Users/dev/Library/Application Support/typora-user-images/Screen Shot 2022-01-31 at 1.04.36 PM.png)

***

### ¬ ArrayLists

**(`import java.util.ArrayList`)**

* The ArrayList is a resizable array where elements can be added and removed from an ArrayList whenever you want.
* Recall that arrays' size cannot be modified (if you wanted to add/remove elements, you'd have to create a new one)

**`Declaration`**

* Creating an ArrayList object: `ArrayList<TYPE> NAME = new ArrayList<TYPE>();`

```
import java.util.ArrayList;   // import the ArrayList Class

ArrayList<Integer> numbers = new ArrayList<Integer>();
ArrayList<String> cars = new ArrayList<String>();
```

**`Initialization` - you can pass an iterable in the declaration using the Arrays.asList( item1 , ... , itemN )**

```
// you'll need to import the Arrays + ArrayList packages
import java.util.ArrayList;
import java.util.Arrays;

ArrayList<Integer> numbers = new ArrayList<Integer>(1, 2, 3);
ArrayList<String> cars = new ArrayList<String>("Sheldon", "Leonard", "Howard", "Raj");
```

**`Add Items` - add()**

```
// LISTNAME.add(ITEM);

numbers.add(1);
numbers.add(2);
numbers.add(3);   // now numbers= [1, 2, 3]

cars.add("Maserati");
cars.add("BMW");
cars.add("Ferrari");    // now cars= ["Maserati", "BMW", "Ferrari"]
```

**`Printing Lists` - unlike arrays, you can simply println arraylists:**

```
ArrayList<Integer> numbers = new ArrayList<Integer>(1, 2, 3);
System.out.println(numbers);    // [1, 2, 3]
```

**`Getting Index of Items` - indexOf()**

* `indexOf()` returns the first occurence of the specified item in the list, otherwise returns -1:

```
// LISTNAME.indexOf("ITEM");

numbers.indexOf(1);          // 0 ; 1 is at index-0 in the numbers list
cars.indexOf("Tesla");      // -1 ; "Tesla" isn't in the cars list 
```

**`Checking for Item` - contains()**

* To check the existence of an item in a list, use the `contains()` method, which returns true/false:

```
// LISTNAME.contains("ITEMS");

numbers.contains(3);          // true
cars.contains("Hyundai");     // false ; "Hyundai" isn't in the cars list 
```

**`Accessing Items` - get()**

* To access an element in the list, use the `get()` method and refer to the index number:

```
// LISTNAME.get(INDEX);

numbers.get(0);   // 1
cars.get(2);      // "Ferrari"
```

**`Changing Items` - set()**

* To modify an element, use the `set()` method and refer to the index number and the new element:

```
// LISTNAME.set(INDEX, "NEWVALUE");

numbers.set(0, 23);              // now, numbers= [23, 2, 3]
cars.set(0, "Infiniti");      // now, cars= ["Infiniti", "BMW", "Ferrari"]

// make sure the index you are trying to change exists and that the new value is the same type as the list type
```

**`Removing Items` - remove() , clear()**

* To remove an element, use the `remove()` method and refer to the index number:
* To remove all elements in the list, use the `clear()` method:

```
// LISTNAME.remove(INDEX);
numbers.remove(2);       // now, numbers= [1, 2]
cars.remove(1);         // now, cars= ["Maserati", "Ferrari"]


// LISTNAME.clear();
numbers.clear();  // list is now empty
cars.clear();
```

**`Size` - size()**

* To find out how many elements an ArrayList have, use the `size()` method

```
// LISTNAME.size();
numbers.size();       // returns 3
cars.size();         // returns 3
```

**`Sorting List (+reverse)`**

* `import java.util.Collections;`
* use the 'Collections' class to `sort()` lists **alphabetically** (_uppercase take priority over lowercase_) or **numerically** (_least to greatest_)
* To sort in **reverse order** {_greatest to least_} and {_descending alphabetical order_}, add _**Collections.reverseOrder()**_ to the _**Collections.sort()**_ call as a second argument:

```
import java.util.ArrayList;
import java.util.Collections;

/* Assume:
    'nums' = [3, 7, 8, 2, -1, -10, 0]
    'cars' = ["Volvo", "BMW", "Ford", "aye"]
*/

// sort list
Collections.sort(nums);     // now, nums= [-10, -1, 0, 2, 3, 7, 8]
Collections.sort(cars);     // now, cars= ["BMW", "Ford", "Volvo", "aye"]

// reverse sort list 
Collections.sort(nums, Collections.reverseOrder());     // now, nums= [100, 8, 7, 3, 2, 0, -1, -10]
Collections.sort(cars, Collections.reverseOrder());     // now, cars= ["aye", "Volvo", "Ford", "BMW"]
```

**`Iterating Through List`**

* There are two ways of looping through a list: a _**for-loop**_, and a _**for-each**_ loop:

```
// for-loop is useful when you need to make use of the index feature.
for (int i = 0; i < cars.size(); i++) {
    System.out.println(cars.get(i));
}


// for-each loop is more convenient and quicker as it doesn't need indices.
for (String i : cars) {
      System.out.println(i);
}
```

***

### ¬ Stacks

**(`import java.util.Stack`)**

* Stacks are an abstract data type with a bounded(predefined) capacity.
* To help visualize Stacks, parallel it to a stack of video games, where the first element added to the stack is at the bottom. Every time you add a video game, it gets added ontop of the stack.

**`Declaration`**

```
// To declare a Stack, include the type of the content it will hold (Integer, String, etc..) and the Stack name followed by new LinkedList<>():

Stack<_Type_> _name_ = new Stack<_Type_>();
Stack<String> games = new Stack<String>();
```

**`Adding to Stack`**

```
// to add to stack, stackName.add(x);
// Note that the first thing added is at bottom of stack

games.add("Call of Duty");
games.add("Genshin Impact");
games.add("Pokemon");
//the games stack from bottom to the top:  "Call of Duty", "Genshin Impact", "Pokemon"
```

**`Accessing Values`**

```
// to get a value from stack, stackName.get(index)
// where index 0 is the bottom

games.get(0);   //"Call of Duty"
games.get(1);   //"Genshin Impact"
games.get(2);   //"Pokemon"
```

**`Removing from Stack`**

```
// for the stack data structure you can only remove the element at the top (last element in stack)
// to do so, use stackName.pop();

games.pop();      // pop() popped the top element out (pokemon) and now leaves us with "Call of Duty","Genshin Impact"
games.pop();     // "Call of Duty"
games.pop();    // Empty now
```

**`Peeking`**

```
//to simply see the top (last element) of the stack- but not remove it, use stackName.peek();

games.peek();   // "Pokemon"
```

**`Check for Element`**

```
//return true/false whether or not the element specified is in the stack; using stackName.contains(x);

games.contains("Genshin Impact");   //true
games.contains("Assassins Creed");   //false
```

**`Check If Empty`**

```
//to check if stack is empty, stackName.empty(). returns true or false

games.empty();   //false
```

**`Size`**

```
//to check how many elements are in the stack (size), use stackName.size()

games.size();   // 3

games.pop();
games.size();   // 2; pop() removed the top element
```

***

### ¬ Queues

**(`import java.util.Queue` | `java.util.LinkedList`)**

* Java Queues order elements in a FIFO (First In First Out) manner. In FIFO, first element is removed first and last element is removed at last.
* To help visualize Queues, parallel it to a line at backyard bbq (or anything where people line up for something), where you give bbq to the person infront of the line. After, they've been served, they leave the line. Queues work in just that way!

**`Declaration`**

```
// To declare a Queue, include the type of the content it will hold (Integer, String, etc..) and the queue name followed by new LinkedList<>():
Queue<Type> queueName = new LinkedList<>();

Queue<Integer> numbers = new LinkedList<>();
Queue<String> bbqLine = new LinkedList<>();
```

**`Adding to Queue`**

```
// to add to queue, queueName.add(x)
// Note that the first thing added is first in Queue

numbers.add(24);
numbers.add(23);
numbers.add(32); // 24,23,32

bbqLine.add("Kobe");
bbqLine.add("Jordan");
bbqLine.add("Shaq"); // "Kobe", "Jordan", "Shaq"
```

**`Removing from Queue`**

```
// to remove from queue, queueName.poll()
// removes first thing in queue; which is 24 (numbers) and Kobe (bbqLine)

numbers.poll(); // 23,32
bbqLine.poll(); // "Jordan", "Shaq"
```

**`Peeking`**

```
// to simply see the 'head' (first element) of queue- but not remove it, use queueName.peek();

numbers.peek(); // 24
bbqLine.peek(); // "Kobe"
```

**`Size of Queue`**

```
//returns amount of things in queue

numbers.size(); // 3
bbqLine.size(); // 3
```

**`Check for Element`**

```
//return true/false whether or not the element specified is in the list; using queueName.contains(x)

numbers.contains(23);   //true
numbers.contains(30);   //false

bbqLine.contains("Jordan");   //true
bbqLine.contains("Curry");   //false
```

**`Convert to Array`**

```
//to convert a queue to an array of the same type, use toArray() method like so:

numbers.toArray();    //numbers is now [24, 23, 32] where 24 is index 0
bbqLine.toArray();    //bbqLine is now ["Kobe", "Jordan", "Shaq"] where kobe is index 0
```

**`Iterating Queue`**

```
// There are multiple ways to iterate through Queues
// Method 1: convert queue to array and traverse via for-each loop:

numbers.toArray();
for (Integer n : numbers) {
    System.out.println(n);
}

// Method 2: Queues also have an inbuilt iterator which can be used to iterate through the Queue.
// First,                     import java.util.Iterator;
// Create iterator object:    Iterator<Type> iteratorName = queueName.iterator();

Iterator<Integer> itr = numbers.iterator();

// hasNext() returns true if the queue has more elements
while (itr.hasNext()) {
    System.out.println(itr.next()); // next() returns the next element in the iteration
}
```

***

### ¬ HashMaps

**(`import java.util.HashMap`)**

* Hashmaps store items in key/value pairs (equivalent of Python's Dictionaries)
* HashMap is known as HashMap because it uses a technique called _**Hashing**_ - technique of converting a large String to a small String that represents the same String. A shorter value helps in indexing and faster searches
* In ArrayLists, you learned that Arrays store items as an ordered collection, and you have to access them with an index number. A Hashmap however, stores items in "key/value" pairs where you can access the 'value' if you provide the 'key'.

Hashmaps can store different types:

* (**String** keys && **Integer** values) or the same type (**String** keys && **String** values)

**`Creating a Hashmap`**

```
// Syntax of creating hashmap:    HashMap<Key Type, Value Type> hashmapName = new HashMap<Key Type, Value Type>();

HashMap<String, String> capitalCities = new HashMap<String, String>();
HashMap<String, Integer> people = new HashMap<String, Integer>();
```

**`Adding to Hashmap`**

```
// to add items to it, use the 'put()' method and specify the key followed by the value:

capitalCities.put("England", "London");
capitalCities.put("Germany", "Berlin");

people.put("LeBron", 35);
people.put("Kobe", 42);

//remember the type of the key&value have to correspond to the order you declared in the HashMap<Key type, Value Type> respectively
```

**`Accessing Items`**

```
// To access a value in the HashMap, use the get() method and refer to its key:

capitalCities.get("England");   //checks capitalCities for key:"England" and returns value:"London"
people.get("Kobe");             //checks people for key:"Kobe" and returns value:42
```

**`Removing Items`**

```
// To remove an item, use the remove() method and refer to the key:

capitalCities.remove("England");    //removes the England/London pair
people.remove("LeBron");            //removes the Lebron/35 pair


// To remove all items, use the clear() method:

capitalCities.clear();
people.clear();
```

**`Replacing Values`**

```
// To replace a value, use the replace() method and provide the old value's key and the new Value:

capitalCities.replace("England", "newCapital");      //replaces England/London pair with England/newCapital
people.replace("LeBron", 27);                       //replaces Lebron/35 pair with Lebron/27
```

**`Retrieving`**

```
// To retrieve all the keys in the Hashmap:

capitalCities.keySet();     // ["England", "Germany"]
people.keySet();            // ["LeBron", "Kobe"] 


// To retrieve all values in the Hashmap:

capitalCities.values();     // ["London", "Berlin"]
people.values();            // [35, 42]
```

**`Checking for Key/Value`**

```
// To check if the Hashmap has a specific Key (returns true/false) :

capitalCities.containsKey("Vietnam");     // False
people.containsKey("LeBron");            // True


// To check if the Hashmap has a specific Value (returns true/false) :

capitalCities.containsValue("Berlin");      // True
people.containsValue(23);                  // False
```

**`Size`**

```
// To find out how many items there are, use the size method:

capitalCities.size();     // 2
people.size();            // 2
```

**`Looping over HashMap`**

```
// Use a for-each loop to iterate through the items of a HashMap.
// Note: Use the keySet() for only the keys, and the values() for only the values:

// Print keys
for (String i : capitalCities.keySet()) {
    System.out.println(i);
}

// Print values
for (String i : capitalCities.values()) {
  System.out.println(i);
}
```

***

## OOP

OOP stands for **Object-Oriented Programming**.

* **Procedural Programming** - writing procedures or methods that perform operations on the data.
* **Object-Oriented Programming** - creating objects that contain both data and methods
* [Naming conventions](https://www.javatpoint.com/java-naming-conventions)

#### `Container Class vs. Definition Class`

_**Container Class**_ - a collection of static methods that aren't bound to any particular object. These static methods usually have something in common.

* The `Math` class is an example of a _container class_. It's essentially a **container** for math utility methods. _**Notice that you call these static methods with dot notation:**** ****`<ContainerClass>.<StaticMethod`**** ****ie.**** ****`Math.sqrt()`**_
* However, for even moderately complex programs a large collection of methods can quickly becomes difficult to manage

_**Definition Class**_ - these classes define new objects. _**`THIS IS THE FOCUS IN CPS209`**_

#### Classes & Objects

_**`¬ Class`**_

* used to define a _new data type_ aka a blueprint for creating objects.
* Each class contains **fields / attributes** (_variables_) and **behaviours** (_methods_).
* The ClassName should always _start with an uppercase first letter_ and _match the name of the java file_.
*   **To create a class, use the `class` keyword:**

    ```java
    public class Animal {
          ...
    }
    ```
* _**`CLASS - an abstract view`**_
  * We usually begin by creating an abstraction of a Class:
    1. What does an object of this class represent?
    2. What's the interface (methods) of this class?
       * The class interface is realized via **methods**
    3. What's the internal state of the class?
       * We use **variables/fields** to represent the internal state.
  * EX. Consider the Abstract view of a Clock Class
    1. A `Clock` class object represents a 12-hr clock
    2. It's interface (methods) allow telling the clock that a second has elapsed (one method for this), and querying the clock to retrieve the time (one for this).

**`¬ Object`**

* a specific **instance** of a class with defined _attributes_.
* the `new` keyword is used to create an _object_ instance of a class. \[ `ClassName objName = new ClassName(params)`]
*   **To create an object:**

    ```java
    class Animal {
      ...
    }

    public class Main {
          public static void main(String[] args) {
              Animal cat = new Animal();       // create new object
              // you can create many objects in one line if they're all the same type (like other type vars)
              Animal dog = new Animal(),
                           fish = new Animal(),
                           lion = new Animal();
          }
    }
    ```
* _**`Object References`**_
  * Object reference variables store the location of an object in memory, not the object itself. That is, the _**`new`**_ operator returns the location (a memory address) of the new object and stores this location in the reference variable.
  *   Multiple reference variables can refer to the same object:

      ```java
      Clock clock1 = new Clock();
      Clock clock2 = clock1;
      // now clock2 and clock1 refer to the same object.
      ```
  * In memory, the addresses of clock1 & clock2 reference variables hold the same address of the Clock Object (ie. 0x7104).
  * _**`Null Reference`**_
    * A reference variable may be set to point to no object at all (_**null**_)
    *   You can't call methods of an objcet using a refernce variable that's pointing to null; _Causes a run-time error_

        ```java
        Clock clk = null;
        int seconds = clk.getSeconds(); // Runtime error!! 

        // Sometimes, check if a reference is null before using it:
        if (clk != null) {
        		...
        }
        ```
  * _**`Garbage Reference`**_
  *
    *   Reference vars. that's aren't initialized refer to random locations in memory; You can only call methods using the Reference var. if it is referring to a valid object

        ```java
        Clock clk; // not referring to valid object
        int seconds = clk.getSeconds(); // Runtime error!!
        ```

**Constructors**

* **special method** that's used to initialize objects.
* The constructor is called when an object of a class is created, and is used to initialize the attributes in a newly created object.
* The line of code which defines the constructor name and other info is called the _**constructor signature**_.
* Rules for creating constructors:
  * _**must have the same name as the class**_
  * **cannot have a return type (void)**\*
  * _**cannot be abstract, static, or final**_
  * (can still be private, protected, public or default)

1.  _**`Default (No-Argument) Constructor`**_ - created by default by the java compiler at the time of class creation if no other constructor is declared in the class. Doesn't contain any parameters

    ```java
    // syntax for default constructor:
    <class_name>() {
      ...
    }
    ```

    ```java
    // Ex.
    class Animal {
        Animal() {     // default constructor    
              System.out.println("New Animal object was created!");
        }

          public static void main(String args[]) {
                   Animal dog = new Animal();
          }
    }
    ```
2.  _**`Parameterized Constructor`**_ - contains one or more parameters used to initialize attributes

    ```java
    class Animal {
          // class attribute
        String name;
          int age;

          // parameterized constructor intializes above-attributes
        Animal(String name, int age) {
            this.name = name;
              this.age = age;
        }
    }
    ```

**Overloading Parameterized Constructors**

* You can _**overload**_ parameterized constructors
*   Basically: multiple constructors with same name but different parameters; different ones get called when creating an object depending on which parameters are passed

    ```java
    class Animal {
        String name; // instance variables
          int age;

        Animal(String name) { // gets called if only a String is passed=> new Animal("name")
            this.name = name;
        }

        Animal(String name, int age) { // gets called if String & int are passed=> new Animal("name", 18)
            this.name = name;
              this.age = age;
        }
    }
    ```

**Constructors vs. Normal Methods**

| Constructor                                                                                | Method                                                  |
| ------------------------------------------------------------------------------------------ | ------------------------------------------------------- |
| used to initialize the instance variables of an object.                                    | used to expose the behavior of an object.               |
| must be void.                                                                              | doesn't have to be void.                                |
| invoked implicitly (when object is created).                                               | invoked explicitly (you have to call it).               |
| Java compiler provides a default constructor if you don't have any constructor in a class. | The method is not provided by the compiler in any case. |
| constructor name must be same as the class name.                                           | can be named anything.                                  |

**Instance Variables**

*   A variable which is created inside the class but outside constructors/methods is known as an _**instance variable**_.

    ```java
    class Car {
          // 'private' instance variables
          private double miles;
        	private String company;

          // instance variables are in the class, but outside the constructor
          Car(double miles, String company) {
              this.miles = miles;
              this.company = company;
        }
    }
    ```
*   You can acess and update instance variables (which aren't 'final') using _**`dot notation`**_:

    ```java
    Test car1 = new Test(2_000, "BMW");

    car1.miles += 1000.5;

    System.out.println( car1.miles );        // 3000.5
    System.out.println( car1.company ); // BMW
    ```
* **Ways to Initialize Objects**
  1.  via assigning values to instance variables manually with dot notation:

      ```java
      class Student{  
            int id;  
              String name;  
      }  

      class TestStudent2{  
               public static void main(String args[]){  
                    Student s1=new Student();  

                // assign values to instance variables manually
              s1.id=101;  
              s1.name="Bruno Mars";  

              System.out.println(s1.id+" "+s1.name); // 101 Bruno Mars
               }  
      }  
      ```
  2.  via setter methods:

      ```java
      class Student{  
               int rollno;  
               String name;  

            void insertRecord(int r, String n) {   // SETTER
                    rollno = r;  
                    name = n;  
               }  

            void printInfo() {     // handy method to print info
            System.out.println(rollno + " " + name);
          }
      }  
      class TestStudent4{  
               public static void main(String args[]){  
                    Student s1=new Student();  
                       s1.insertRecord(101,"Frank Ocean");   // call setter method
                      s1.displayInformation();   // 101 Frank Ocean
               }  
      }  
      ```
  3. via constructor (most common)

**Static Methods**

* methods which have the `static` keyword in their signature _belong to a class rather than an instance of a class_.
* Static methods can only reference static variables or local variables (within the method)
* _Static methods_ can't read/set instance variables because they can't refer to _this_ or _instance variables_ since they're called with the CLASSNAME, not an OBJECT.
*   You can call it without creating an object; They are called by the **class name itself**: `<className>.<staticMethod>();`. If you're referencing static variables/methods in the same class, treat them with global scope.

    ```java
    public class Display {  
            public static void main(String[] args) {  
                    Display.show();  
              // or simply: 'show()' since they're in the same class
            }  

          static void show() {  
                    System.out.println("It is an example of static method.");  
            }  
    }  
    ```

**Instance Methods**

* The method of the class is known as an **instance method**.
* It's a **non-static** method defined in the class.
* Unlike _**static methods**_, _**instance methods**_ can access _**static variables**_.
*   Before calling or invoking the instance method, it is **necessary to create an object of its class**

    ```java
    public class Car {  
        int miles;  // instance variables

        // instance method  
        public int getMiles() {  
          	return this.miles; 
        }

      	public static void main(String [] args) {
    				// Create an object of the class  
            Car ferrari = new Car(6_000);
            // invoking instance method   
            sysout("This car has: " + ferrari.getMiles());
        }  
    }  
    ```
* There are 2 types of instance method:
  1. **Accessor Method** (GETTER)
     * Methods used to get instance variables
     * Usually prefixed with **'get'**
     *   Asks the object for info and normally returns a value of some variable

         ```java
         public int getMiles() {
                 return this.miles;    
         } 
         ```
  2. **Mutator Method** (SETTER)
     * Methods used to update values of instance variables usually prefixed with **'set'**
     * Return type is normally _**`void`**_.
     *   Usually take a parameter that will change an instance variable.

         ```java
         public void addMiles(int addMileage) {  
                 this.miles += addMileage;  
         } 
         ```

### this

* The keyword **this** can be used in a class to refer to the current calling object
*   'this' is used in the constructor to set the instance variables.

    ```java
    public class Student {
    		private int id;
    		private String name;
    		
      	public  Student(int id, String name) {
    				this.id = id;  // set values of instance variables
    				this.name = name;
    		}
    }
    ```
* _Static methods_ cannot refer to _this_ or _instance variables_ because they are called with the classname, not an object, so there is no this object.
*   You may invoke the method of the current class by using the this keyword:

    ```java
    class A {  
        void m() { System.out.println("hello m"); }  
        void n() {
          	System.out.println("hello n");
            this.m();    // when object 'a', this.m() == a.m()
        }  
    }  

    class B {  
        public static void main(String args[]) {  
          	A a = new A();       // create object 'a'
    				a.n();              // call the n() instance method
        }
    }  
    ```

### 4 Pillars of OOP

#### 1. _Encapsulation_

* **process of wrapping code and data together into a single unit.**
* **The goal is to make sure that "sensitive" data is hidden from users.**
* This is achieved via:

**Packages**

* A **java package** is a group of similar types of classes, interfaces and sub-packages. (Think of it as **a folder in a file directory**)
* We use packages to avoid name conflicts, and to write a better maintainable code (modularize code).
* Packages are divided into two categories:
  1. _`Built-in`_ Packages (packages from the Java API)
  2. _`User-defined`_ Packages (create your own packages)
* To create a package:
  1.  use the **`package`** keyword:

      * The package name should be written in lower case to avoid conflict with class names

      ```java
      // save as MyPackageClass.java  
      package mypack;
      class MyPackageClass {
            public static void main(String[] args) {
                  System.out.println("This is my package!");
            }
      }
      ```
  2.  Save the file as **MyPackageClass.java**, and compile the file:

      ```
      $ javac MyPackageClass.java
      ```
  3.  Compile the package:

      * This forces the compiler to create the "mypack" package.
      * The `-d` keyword specifies the destination for where to save the class file (**.** is current working directory)

      ```
      $ javac -d . MyPackageClass.java
      ```
  4. When we compiled the package above, a new folder was created, called "mypack".

**Access Modifiers**

* access modifiers specify the scope of a field (variable), method, constructor, or class.
* There are many **non-access** modifiers, such as static, abstract, synchronized, native, volatile, transient, etc
*   A _**`member`**_ is a variable/method/constructor of a class; members of a class can be declared the following 4 access modifiers (listed st. first is most restrictive, and last, the least):

    1. **`Private`**
       * private scope is only within the class; it cannot be accessed from outside the class.
       * If you make any constructor private, you cannot create the instance of that class from outside the class.
       * With Private, we perform _data-hiding_; hide the internal implementation of the class by declaring its state variables and auxiliary methods as private. (Encapsulation)
    2. **`Default`**
       * default scope is only within the package; it cannot be accessed from outside the package.
       * If you do not specify any access level, it will be the default.
    3. **`Protected`**
       * protected scope is within the package and outside the package through child class.
       * If you do not make the child class, it cannot be accessed from outside the package.
    4. **`Public`**
       * public scope is everywhere; it can be accessed from within the class, outside the class, within the package and outside the package.
       * If you don't want to reveal the internal state of the object’s data don't declare its state variables as public. (Encapsulation)

    | Access Modifier | within class | within package | outside package by subclass only | outside package |
    | --------------- | ------------ | -------------- | -------------------------------- | --------------- |
    | **Private**     | Y            | N              | N                                | N               |
    | **Default**     | Y            | Y              | N                                | N               |
    | **Protected**   | Y            | Y              | Y                                | N               |
    | **Public**      | Y            | Y              | Y                                | Y               |

    _**Note**_: If you are overriding any method, the overridden method (ie. declared in subclass) must not be more restrictive

    * ie. you can't override a _protected_ (#3 restrictive) method with a _default_ (#2 restrictive) method since #2 is more restrictive than #3. This causes a compile-time error.



**Providing GETTER(s) & SETTER(s)**

* By providing _**only a getter**_ / _**only a setter**_ method, you can make the class _**read-only**_ / _**write-only**_.
*   This allows for: **more control over the data** , **data hiding** , and **easy testing**.

    ```java
    // READ-ONLY = class w/ only GETTER methods.  (no setters to change it & you can't do s.uni)
    public class Student {
            private String uni = "RU";  // private instance variable

          public String getUni() {  // GETTER method  
          return uni;
        }
    }  
    // Now, you can't change the value of the private instance variable
    ```

    ```java
    // WRITE-ONLY = class w/ only SETTER methods.   (can't do s.uni)
    public class Student {
            private String uni;  // private instance variable

          public void setUni(String uni) {  // SETTER method  
          this.uni = uni;
        }
    }  
    // Now, you can't get the value of the private instance variable, you can only change it.
    ```

#### 2. _Inheritance_

*   Inheritance is a mechanism in which one class can inherit all attributes (variables) & behaviours (methods) of a parent class.

    * **parent class** | | **superclass** - class being _**inherited from**_.
    * **child class** | | **subclass** - class that _**is inheriting**_.

    Inheritance represents the **IS-A relationship** which is also known as a _parent-child_ relationship
* Inheritence is great because it allows: **code reusability** & **runtime polymorphism**.
  * _Code reusability_ = when you inherit from an existing class, _you can reuse attributes and behaviours of the parent class_. Moreover, you can add new attributes and behaviours in your current class.

#### Types of Inheritence

1. **Single - when a class inherits another class. (a -> b)**
2. **Multilevel - when there is a chain of inheritance. (a -> b -> c)**
3. **Hierarchical Inheritance - when two or more classes inherits a single class. (a, b -> c)**

![Types of inheritance in Java](https://static.javatpoint.com/images/core/typesofinheritance.jpg)

#### IS-A vs. HAS-A

_**`IS-A`**_ :

* An IS-A relationship is inheritance. The child class is a type of parent class.
*   static (compile time) binding.

    ```java
    class Apple extends Fruit { 
            // Apple (child) IS-A Fruit (parent)
    }
    ```

_**`HAS-A`**_ :

* A HAS-A relationship is composition; meaning creating instances which have references to other objects.
*   dynamic (run time) binding.

    ```java
    // A Room HAS-A Table. So you create a Room class and create a Table instance. So class Room HAS-A Table
    class Room {
        Table table = new Table();
    }
    ```
* To make a subclass inherit from a superclass, use the **`extends`** keyword:

```java
class childClass extends parentClass {  
           // methods and fields  
          // establishes an IS-A relationship (childClass IS-A parentClass)
}  
```

```java
class Employee {  
      float salary=40000;  // child classes can use behaviours and
}  
class Programmer extends Employee {  // Programmer IS-A Employee
         int bonus=10000;  

      public static void main(String args[]) {  
               Programmer p=new Programmer();  
               System.out.println( "Programmer salary is:" + p.salary );  
               System.out.println( "Bonus of Programmer is:" + p.bonus );  
        }  
}  
```

* **While a person can have two parents, a Java class can only inherit from one parent class. If you don't specify a superclass with 'extends', the class will default-inherit from the `Object` class.**

#### Substitution Principle

* You can always use a _**`subclass object`**_ when a _**`superclass object`**_ is expected as a parameter to a method.

#### Super()

* Subclasses inherit _public methods_ from the superclass that they extend, but they _cannot access the private instance variables_ of the superclass directly and _must use the public GETTERs & SETTERs_.
* Subclasses do not inherit constructors from the superclass
* _**super()**_ solves the quesiton of: "how do you initialize the superclass’ private variables if you don’t have direct access to them in the subclass?"
*   The superclass constructor can be called from the first line of a subclass constructor by using the special keyword **super()** and passing appropriate parameters

    ```java
    // assume a 'Person' class
    public class Employee extends Person {
        public Employee() {
            super();                 // calls the Person() constructor
        }
        public Employee(String theName) {
            super(theName); // calls Person(theName) constructor
        }
    }
    ```
* If a subclass doesn't call the superclass' constructor with _**`super()`**_ as the first line in a subclass constructor then the compiler will automatically add a `super()` call as the first line in a constructor.
* The keyword super can be used to call a superclass’s constructors and force-use its methods.
*   You want to still execute the superclass method, but you also want to override the method to do something else. But, since you have overridden the parent method how can you still call it? There are two uses of the keyword _**`super`**_:

    1. **super();** or **super(arguments);** - calls just the super constructor if put in as the first line of a subclass constructor.
    2. **super.method();** - calls a superclass’ method (not constructors).

    ```java
    public class Base { // PARENT
       public void method1() {
             sysout("A"); // 2
             method2(); // 3; checks if it exists in the subclass (which it does)
       }

       public void method2() {
             sysout("B"); // 5
       }
    }

    public class Derived extends Base { // CHILD
       public void method1() { // called FIRST
          super.method1(); // 1
          sysout("C");
       }

       public void method2() {
           super.method2(); // 4
           sysout("D"); // 6
       }
    }

    /* In a client program:
    Base b = new Derived();
    b.method1();
    */ Prints "ABCD"
    ```



#### Overriding Methods

* We also usually add more methods or instance variables to the subclass.
* **overriding** inherited methods - providing a public method in a subclass with the same **method signature** (name, parameter type list, and return type) as a public method in the superclass.
* The method in the subclass will be called _instead of_ the method in the superclass.
* You may see the _**`@Override`**_ annotation above a method. This is optional but it provides an extra compiler check that you have matched the method signature exactly:
* **NOTE: YOU SHOULD NEVER OVERRIDE VARIABLES. Each object would have two instance fields of the same name. ("Shadow Variable")**

```java
public class Greeter { // Parent
   public String greet() {
      return "Hi"; // instances of Parent class will print this
   }

   public static void main(String[] args) {
      Greeter g1 = new Greeter();
      System.out.println(g1.greet()); // instance of Greeter (parent) : "Hi"

      Greeter g2 = new MeanGreeter();
      System.out.println(g2.greet()); // instance of MeanGreeter (child) : "Fuck outta here"
   }
}

class MeanGreeter extends Greeter { // Child
       @Override
      public String greet() { // Child inherits greet() from Parent, but overrides it
          return "Fuck outta here"; // instances of Child class will print this
       }
}
```

#### Overloading methods

* **Overloading** inherited methods - when several methods have the same name but the parameter types, order, or number are different.

So with overriding, the method signatures look identical but they are in different classes, but in overloading, only the method names are identical and they have different parameters.

#### Superclass References

* A superclass reference variable can hold an object of that superclass or of any of its subclasses.
*   This is a type of **polymorphism**.

    ```java
    // assume: Square, Rectangle -> Shape
    Shape s1 = new Shape();
    Shape s2 = new Rectangle();
    Shape s3 = new Square();

    // the opposite is not true! You can't do:
    Rectangle s4 = new Shape(); // err
    ```

#### Passing subclass objects as parameters

*   We can write methods with parameters of the superclass type and pass in subclass objects to them.

    ```java
    // This will work with all Shape subclasses (Squares, Rectangles, etc.)
    public void someMethod(Shape s) {
       ...
    }
    ```
*   Similar for arraylists:

    ```java
    // This shape array can hold the subclass objects too
    Shape[] shapeArray = { new Rectangle(), new Square(), new Shape() };

    // The shape ArrayList can add subclass objects too
    ArrayList<Shape> shapeList = new ArrayList<Shape>();
    shapeList.add(new Shape());
    shapeList.add(new Rectangle());
    shapeList.add(new Square());
    ```

***

#### 3. _Polymorphism_

* _Poly = many_, _morphism = forms_; so _Polymorphism = many forms_
* **Polymorphism in Java is the ability of an object to take many forms**; allows us to perform the same action in many different ways.
* Any Java object that can pass more than one IS-A test is considered to be **polymorphic** (really all objects in Java which have even just one IS-A, are polymorphic since all Java objects by default, inherit from `Object`)
* JVM looks at type of object the reference variable is pointing to (i.e at run time)and executes the correct method for that object.

1.  It's always OK to convert subclass reference to superclass reference but not other way around.

    ```java
    // Executive --> Employee --> Object

    Executive exec = new Executive();
    Employee empl = exec; // OK
    ```
2.  If you want to convert _`superclass ref. variable`_ to _`subclass`_, you must _**`cast`**_:

    * Make sure superclass ref. variable is referring to a subclass object using the _`instanceof`_ keyword:

    ```java
    // Executive --> Employee --> Object

    Executive exec = new Executive();
    Employee empl = exec;						
    Executive exec2;

    if (empl instanceof Executive)
    		exec2 = (Executive)employee
    ```

***

### Object: The superclass of all classes

* All classes etend Object
* most useful methods in class Object:
  1. _**`String toString()`**_
     * Returns a string representation of the object
     * Useful for debugging
     * ie. toString() in class Rectangle returns something like:
       * _`java.awt.Rectangle[x=5,y=10,width=20,height=30]`_
     *   toString() is used by concatenation operator

         ```java
         // ie
         BankAccount b = new BankAccount(9876543,300);

         // means String test = “xyz” + b.toString();
         String test = “xyz” +  b; 
         ```
     * toString() in class Object returns class name and object address:
       * ie. Employee@d2460bj
     * It's common to _**OVERRIDE**_ the toString() method
  2.  _**`boolean equals(otherObj)`**_

      * _**equals()**_ tests for _`equal contents`_
      * note: _**==**_ tests for _`equal memory locations`_ of objects
      * Must cast the "otherObj" parameter to subclass

      ```java
      if (exec1 == exec2)
      		sysout(“two references to same object”);

      if (exec1.equals(exec2))
      		sysout(“two objects with same name and payrate”);
      ```
  3. clone()

***

#### Abstract Methods and Classes

* When you extend a class, you have the choice to override a method (or not)
* Sometimes want to force the subclass creator to override a method
  * method might be common to all subclasses so should define it in superclass but there is no good default implementation
* You can make the method abstract _**(just signature, no body)**_
  * ie. abstract public double area();
  * Now subclass can implement method area();
* **If a class has >= 1 abstract method, whole class must be made abstract**
  * ie. class is made abstract by: abstract public class BankAccount
* You can’t create objects of abstract classes; abstract classes are used to define a _common interface_ and behavior for all subclasses.
* Abstract classes can have instance variables, abstract methods, concrete methods.
  * A subclass inherits said instance variables and methods. It must then implement abstract methods. If the subclass doesn't implement the abstract method(s), it too becomes abstract
* You can also **prevent** others from creating subclasses and overriding methods using the _`final`_ keyword.

***

### Interfaces

In general terms, an _**interface**_ is a container that stores the signatures of the methods to be implemented in code segments. (it's an outline for a class)

An interface can be thought of as a 'connector' b/n the general methods in the container and your code segments.

**$ Defining**

* An Interface can _only_ have method signatures, fields and default methods (skeleton code). You have to write the code for these methods inside your class.
*   To define an interface, use the _**`interface`**_ keyword:

    ```java
    public interface Measurable {
      	// notice it's an empty body
      	double getMeasure()
    }
    ```

**$ Implementing**

* The interface alone is not of much use, but they're used along with Classes which help further define them.
* Use the _**`implements`**_ keyword to indicate that a class implements an interface type.
*   A class can implement > 1 interface.

    ```java
    // for the above Measurable interface,

    public class Clock implements Measurable {
      	// define the interface method here
      	public double getMeasure() {
          	return balance;
        }
    }
    ```
* There are **ground rules**:
  * The Class must implement _**ALL**_ of the methods in the interface
  * The methods must have the _**exact same signature**_ as described in the interface
  * The class _**doesn't**_ need to declare the fields; only the methods.
  * An interface _**can't**_ contain a constructor method. Therefore, you _**can't**_ create instances of the Interface itself.

**Interfaces vs. Classes**

* An interface type is similar to a class, but there're some important differences:
  1. All methods listed in an interface type are **abstract**;
     * i.e. they don't have any code!!
  2. All methods listed in an interface type are **automatically public**
  3. An interface type **does not have instance variables**!
* Inheritance (Class) defines a _**is-a**_ relationship
  * Strong relationship b/n super and cubclass
* Interface defines a _**has-a**_ relationship:
  * Share some behaviour, but that's all

**Converting b/n Class & Interface types**

*   You can convert an instance variable from a _**class type --> interface type**_, provided the class implements the interface.

    ```java
    // asssume BankAccount implements interface Measurable:

    BankAccount account = new BankAccount(10000);
    Measurable m = account; // CONVERSION is OK

    // after converting, variable m is not of type BankAccount so it can't use it's methods:

    int size = m.getMeasure(); 	// OK
    m.deposit(55.0);			// ERROR
    ```
*   To convert the instance variable from a _**interface type --> back to --> class type**_, use _**(casting)**_:

    ```java
    // compiler will throw error if m isn't referring to a BankAccount object
    BankAccount b = (BankAccount) m;
    b.deposit(55.0);
    ```

### Polymorphism & Interfaces

*   Interface reference variable holds reference to object of a class that implements the interface:

    ```java
    Measurable m;
    m = new BankAccount(10000);
    ```
* Note:
  * the object to which m points to _**is not of type Measurable**_**.** It's type is the class that implements the Measurable interface (BankAccount).
  * The variable m itself _**is of type Measurable**_
* Say two classes BankAccount & Clock both implement Measurable interface. Each class will have their own implementation of the getMeasure().
  * **How will we know whose getMeasure() is being called?**
  * Polymorphism says that it **depends on the actual object**.
  * So if m refers to a BankAccount, it'll call BankAccount's getMeasure(). If it refers to a Clock, then it'll call Clock's getMeasure().
* _**`Polymorphism`**_ - behaviour (methods) can vary depending on the type of the object calling it.
  * "Binding" is the association of a method call with the method definition. There are 2 types of binding:
    1. _**`late-binding`**_ - happens at compile time.
    2. _**`early-binding`**_ - happens at run time.

**Polymorphism vs. Overloading:**

* _**Similarity**_: both describe a situation where one method name can denote multiple methods.
* _**Difference**_:
  * _overloading is resolved early by the compiler_, by looking at the types of the parameter variables.
  * _Polymorphism is resolved late_, by looking at the type of the implicit parameter object just before making the call

***

### Exception Handling & IO

**> Throwing Exceptions**

* Throwing exceptions is the solution to the problem of erroneous functions which may or may not throw errors.
* Exceptions can't be overlooked/ignored and are sent directly to an _**exception handler**_ (not just to the caller of the failed method)
*   You _**THROW**_ an _**EXCEPTION OBJECT**_ to signal an exceptional condition; there's no need to store this object in a variable.

    ```java
    // ie.
    throw new IllegalArgumentException("Amoung exceeds balance");
    ```
* When an exception is thrown:
  1. Method terminated immediately (kinda like 'return')
  2. Excecution continues in an _exception handler_

#### > Checked & Unchecked Exceptions

There are 2 types of exceptions:

1. _**Checked**_ - _**compiler**_ checks that you don't ignore them
   * they're due to external circumstances that the programmer can't prevent ie. User I/O
   * ie. `IOException`
2. _**Unchecked**_ - extends the class RuntimeException or Error
   * they're typically the programmer's fault
   * Examples of _**runtime exceptions:**_ `NullPointerException`
   * Examples of _**errors:**_ `OutOfMemoryError`

#### > Exception Handlers

*   _**exception handlers**_ are created with _**try/catch**_ blocks

    try - contains statement that may cause an exception

    catch - contains handler code to deal w/ particular exception type

```java
try {
    //code block
} catch (Exception e) {
    //code block to handle errors
}

/*
tries the code in the try code block. If it throws an exception, it will instead run the catch{}'s code

Keep the 'e' (object), replace the "Exception" with:
        - ArithmeticException
        - FileNotFoundException
        - ArrayIndexOutOfBoundsException
        - ...
*/

// ie.
Scanner sc = new Scanner(System.in);
System.out.println("Input a integer: ");

String s = sc.next();
int in = 0;

try {
		in = Integer.parseInt(s);
} catch (NumberFormatException e) { 
	  // if a NumberFormatException is thrown
		System.out.println(“Invalid input.”);
		e.printTraceStack();
} catch (ArithmeticException) {
  // you can chain catch-blocks
} finally {
  // do this when try-block is exited in any of the 3 ways:
  // 1. Try-block code was executed (Everything OK)
  // 3. Exception thrown in Try-block and caught in Catch-block
  // 3. Exception thrown in Try-block but not caught
}
```

***

### I/O

*   To read a local file, construct a file object, then use the file object to construct a scanner object:

    ```java
    File f = new File("numbers.txt");
    Scanner sc = new Scanner(f);

    // use Scanner methods to READ from file. ie:
    while (in.hasNextDouble()) {
      	double value = in.nextDouble();
      	// ...
    }
    ```
*   To write to a file, construct a _**`PrintWriter`**_ object

    ```java
    PrintWriter pw = new PrintWriter("output.txt");

    // if the file already exists, IT IS EMPTIED before the new data is written to it (you can, however, also append to the data already on it).

    // if the file doesn't exist, empty file output.txt is created.

    // Use PRINT/LN/F to WRITE into PrintWriter:
    pw.println("WuTang Clan ain't nun to fuck wit!");
    pw.printf("Total: %8.2f/n", total);
    ```
*   You must close a file after you're done processing it:

    ```java
    pw.close() // close PrintWriter
    sc.close() // close Scanner
    ```

**Handling FileNotFoundException**

* When a FileNotFoundException occurs (thrown by the File constructor), you have 2 choices:

1. Handle the exception inside the method (with a try-catch)
2.  Tell the compiler that you want the method to be terminated when the exception occurs.

    * The **throws** keyword indicates that the method will \[potentially] throw a CHECKED EXCEPTION. For multiple exceptions, just separate with comma:

    ```java
    // method will terminate if any FileNotFound or IO exception occurs:

    void myMethod() throws FileNotFoundException, IOException {
    		String filename = “myFile.txt”; 
    		File inputFile = new File(filename); 
    		Scanner in = new Scanner(inputFile);
    		// ...
    }
    ```

    * Keep in mind the _**INHERITANCE HIERARCHY**_ for exceptions; if a method can throw IOException & FileNotFoundException, we know that FileNotFound inherets from IO therefore, only use IOException.

**Catching Exceptions**

```java
catch (IOException e) {...}

// e -> exception reference variable contains reference to the exception object thrown.
  
// catch-block -> can analyze object to find out info

// e.printStackTrace() -> printout of chain of method calls that lead to exception.
```

**Creating Custom Exception Types**

* You can design your own exception types (subclasses of Exception or RuntimeException)
* Make it an UNCHECKED exception
* Extend RuntimeException or one of its subclasses
* Supply 2 constructors:
  1. default constructor
  2. constructor that accepts a message string describing reason for exception

```java
public class CustomException extends RuntimeException {
  	
  	public CustomException() {...} // 1
		
  	public CustomException(String message) { // 2
      	super(message);
    }
}
```

***

### Collections

A _**collection**_ is simply an object that represents a group of objects into a single unit.

_**`Collection Framework`**_ - a unified architecture or a set of classes and interfaces for representing and manipulating collections. i.e. collection framework is used to store, retrieve and manipulate collections.



#### > Lists & Sets

* A **list** is a collection that maintains the order of its elements
* Ordered Lists:
  * _ArrayList_ –– stores a list of items in a dynamically sized array
  * _LinkedList_ –– allows speedy insertion and removal of items from the list
* A **set** is an unordered collection of unique elements.
* Unordered Sets:
  * _HashSet_ –– uses hashtables to speed up finding/adding/removing elements
  * _TreeSet_ –– uses a binary tree to speed up finding, adding, and removing elements

#### > Stack & Queues & PriorityQueues

* Another way of gaining efficiency in a collection is to reduce the number of operations available. 2 examples are:
  * _Stack_ –– remembers the order of its elements, but it does not allow you to insert elements in every position. You can only add and remove elements at the top.
  * _Queue_ –– add items to one end (the tail), remove them from the other end (the head).
  * _PriorityQueues_ –– collects elements, each of which has a priority. Remove lowest number first



#### > Maps

* A **map** stores keys, values, and the associations between them
* _Keys_ –– provides an easy way to represent an object
* _Values_ –– actual object associated with the key

#### > LinkedList

* use references to maintain an ordered lists of **nodes**.
  * The **head** of the list references the first node.
  * Each **node** has a **value** and a **reference** to the next node.
* Efficient Operations
  * _Insertion_ of a node –– Find the elements it goes between. Remap the references.
  * _Removal_ of a node –– Find the element to remove. Remap neighbor’s references
  * _Visiting_ all elements in order
* Inefficient Operations
  * _Random access_.

***

### Iterators

#### List Iterators

*   When traversing a LinkedList, use a _**ListIterator**_ to:

    * keep track of where you are in the list.
    * access elements inside a linked list.
    * visit other than the first and the last nodes.

    ```java
    ListIterator<String> iter = myList.listIterator()
    ```

&#x20;

Note:

* When calling .add(...) ,
  * the new node is added AFTER the Iterator.
  * the Iterator is moved past the new node.
* When calling .remove() ,
  * it removes the object that was returned with the last call to next or previous.
  * it can be called only once after next or previous.
  * You cannot call it immediately after a call to add.
