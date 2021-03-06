## Notes on Chapter 1: Basic JavaScript: Values, Variables and Control Flow

### Values

There are six basic types of values: **numbers**, **strings**, **Booleans**, **objects**, **functions** and **undefined** values

### Numbers

The standard describes JavaScript numbers as 64-bit floating-point values (e.g. 144 might look like 0100000001100010000000000000000000000000000000000000000000000000 in bits). This means they can also contain fractions and exponents. More details here: http://grouper.ieee.org/groups/754/
Calculations with integers that fit in 52 bits are guaranteed to always be precise, unlike calculations with fractional numbers.

### Strings

Whenever a backslash (\\) is found inside quoted text, it indicates that the character after it has a special meaning: "A newline character is written like \"\\n\"."

### Unary operators

The operators that operate on two values, such as **+** or __*__ are called _binary_ operators; the **typeof** operator (e.g. <code>typeof 4.5</code> -> "number") is a _unary_ operator. **-** can be used both as a unary and a binary operator.

### Boolean Values, Comparisons, and Boolean Logic

Comparing strings is more or less alphabetic. <code>"Aardvark" < "Zoroaster"</code> -> true. Uppercase letters are always "less" than lowercase ones ("Z" < "a") and nonalphabetic characters (!, @, etc.) are also included in the ordering. The actual way in which the comparison is done is based on the _Unicode_ standard. This standard assigns a number to virtually every character one would ever need, including characters from Greek, Arabic, Japanese, Tamil, and so on.

### Variables

Digits can be part of variable names, as well as the __$__ and **_** characters. <code>catch22</code> or <code>$_$</code> are correct variable names.

### Automatic Type Conversion

When comparing values that have different types, JavaScript tries to convert one of the values to the type of the other value: <code>"" == 0</code> -> true, <code>"5" == 5</code> -> true. The rules for converting strings and numbers to Boolean values state that 0, NaN and the empty string count as false, while all the other values count as true.

When you do not want automatic type conversion to happen, there are two extra operators: !== and === (it tests if a value is _precisely_ or not equal to the other)

All arithmetic operations on the value NaN result in NaN (e.g. <code>"strawberry" * 5</code>). Also, <code>NaN == NaN</code> -> false