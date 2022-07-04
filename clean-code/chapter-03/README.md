# Chapter03
## Functions

Tips to writing great functions
### 1. Small
- Should be at maximum 20 lines long.
- The blocks within `if`, `else`, `while`, and so on should be one line long. Probably that line should be a function call.
- The nested structures (blocks) should be one or two at maximum.

### 2. Do One Thing
- Functions should do ONE thing. They should do it WELL. They should do it ONLY.
- To know the function do one thing or not, try to describe it as an only one TO paragraph
- Functions that do one thing cannot be reasonably divided into sections.

### 3. One Level of Abstraction per Function
- The Stepdown Rule (Reading Code from Top to Bottom): make your code reads like a top-down story (top-down set of TO paragraphs).
- To do that, should every function written in a single level of abstraction and followed by the next function in the next level of abstraction, and the third one in the third level of abstraction, and so on. 

### 4. Switch Statements
- Insert switch statement in a class and never repeated again in your code.

### 5. Use Descriptive Names
- Don't be afraid to make a name long. A long descriptive name is better than a short unclear name. A long descriptive name is better than a long descriptive comment.
- Don't be afraid to spend time choosing a name.
- Choosing descriptive names will clarify the design of the module in your mind and help you to improve it.
- Be consistent in your names. Use the same phrases, nouns, and verbs in the function names that you choose for your modules.

### 6. Function Arguments
- The ideal number of arguments for a function is 0.
- 3 arguments should be avoided as possible.
- More than 3 requires a special justification and shouldn't be used anyway.

**Monadic Functions (1 argument)**
- There are 3 forms to pass a single argument into a function:
    + Function that asking a question about that argument: eg. `boolean fileExists("MyFile")`
    + Function that transforming the argument into something else and returning it: eg. `InputStream fileOpen("MyFile")` transforms a file name type `String` into an `InputStream` return value.
    + Function is an event: there is an input argument but no output argument, and the function use the argument to alter the state of the system: eg. `passwordAttemptFailedNtimes(int attempts)`

**Flag Arguments (Boolean arguments)**
- Flag arguments are confusing and should be eliminated if possible.
- It complicates the signature of the function. It makes the function does more than one thing, one thing if the flag is true and another if the flag is false.

**Dyadic Functions (2 arguments)**
- There are times where 2 arguments are appropriate like `Point p = new Point(0, 0)` because the points naturally take 2 arguments x and y.
- It will be better to find mechanism to convert the dyadic function to monadic (in some cases if possible).
- For example, `writeField(outputStream, name)` can convert to monadic by any one of these methods:
    + Make the `writeField` a member function of `OutputStream` class so that you can say `outputStream.writeField(name)`
    + Make the `outputStream` a member variable of the current class so that you don't have to pass it, like this `writeField(name)`.

**Triads Functions (3 arguments)**
- Function that take 3 arguments are significantly harder to understand than dyadic. You should think very carefully before creating a triad.

**Argument Objects**
- When a function seems to need more than 2 or 3 arguments, then, it is likely that some of those arguments should be wrapped into a class of their own.
- For example:
```java
Circle makeCircle(double x, double y, double radius);
```
can be wrapped to
```java
Circle makeCircle(Point center, double radius);
```

**Argument Lists**
- Sometimes we want to pass a variable number of arguments into a function.
- If the variable arguments are all treated identically, then they are equivalent to a single argument of type `List (Object...)`
- For example:
```java
String.format("%s worked  %.2f hours", name, hours);
```
Then the declaration for this function will be:
```java
public String format(String format, Object ... args);
```
- Functions that take variable arguments can be monads, dyads, or triads. And it would be a mistake to give them more arguments than that.
```java
void monad(Integer ... args);
void dyad(String name, Integer ... args);
void triad(String name, int count, Integer ... args);
```

**Verbs and Keywords**
- In case of a monad, the function and argument should form a very nice verb/noun pair that preferred to used as the function name and this called keyword form. For example, the function `writeField(name)`, which tells us that the `name` thing is a `Field`.
- We can encode the names of the arguments directly into the function name. For example, `assertEquals(expected, actual)` might be better written as `assertExpectedEqualsActual(expected, actual)`. This reduce the problem of having to remember the ordering of the arguments.


### 7. Have No Side Effects
- Side effects mean that your function promises to do one thing, but it also does other hidden things.
- Try to avoid these things because they leads to a temporal couplings (kind of coupling).

**Output Arguments**
- Arguments are often interpreted as inputs to a function, but sometimes interpreted as an outputs.
- Output arguments should be avoided. If your function must change the state of something, have it change the state of its owning object.

### 8. Command Query Separation:
- Functions should either do something or answer something, but not both.
- For example: this function sets the value of a named attribute and returns true if it is successful and false if no such attribute exists.
```java
if (set("username", "uncleBob")) {
    ...
}
```
It should separate the command from the query.
```java
if (attributeExists("username")) {
    setAttribute("username", "uncleBob");
    ...
}
```

### 9. Prefer Exceptions over Returning Error Codes:
- Using exceptions instead of returned error codes, then the error processing code can be separated from the happy path code.

**Extract Try/Catch Blocks**
- Try/catch blocks confuse the structure of the code and mix error processing with normal processing.
- It is better to extract the bodies of the try and catch blocks out into functions of their own.

**Error Handling Is One Thing**
- Functions should do one thing. Error handing is one thing. So, a function that handles errors shouldn't do another thing.
- If the keyword `try` exists in a function, it should be the first word in the function and should be nothing after the catch/finally blocks.

**The Error.java Dependency Magnet**
- Returning error codes lead to that there is some class or enum in which all the error codes are defined.
```java
public enum Error {
    OK,
    INVALID,
    NO_SUCH,
    LOCKED,
    OUT_OF_RESOURCES,
    WAITING_FOR_EVENT,
}
```
- Classes like this are a dependency magnet; many other classes must import and use them. Thus, when the `Error` enum changes, all those other classes need to be recompiled and redeployed.

### 10. Don't Repeat Yourself

### 11. Structure Programming
Edsger Dijkstra's rules of structured programming say that every function, and every block within a function, should have one entry and one exit. Following these rules means that there should only be one `return` statement in a function, no `break` or `continue` statements in a loop, and never, ever, any `goto` statements.
