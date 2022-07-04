# Chapter07
## Error Handling

### 1. Use Exceptions Rather Than Return Codes
- It is better to throw an exception when you encounter an error. The calling code is
cleaner.

### 2. Write Your `Try-Catch-Finally` Statement First
- `Try` blocks are like transactions.
- `Catch` blocks should leave your program in a consistent state, regardless of what happens in the `try`.
- Write tests around expected exception handling under certain conditions.

### 3. Provide Context with Exceptions
- Each exception that you throw should provide enough context to determine the source and
location of an error.
- Create informative error messages and pass them along with your exceptions.
- Mention the operation that failed and the type of failure.

### 4. Define Exception Classes in Terms of a Caller’s Needs
- Wrapping third-party APIs is a best practice
- Minimize your dependencies upon it: You can choose to move to a different library in the future without much penalty.
- Wrapping also makes it easier to mock out third-party calls when you are testing your own code.

### 5. Don't Return Null
- If you are tempted to return null from a method, consider throwing an exception or returning a SPECIAL CASE object instead.
- If you are calling a null-returning method from a third-party API, consider wrapping that method with a method that either throws an exception or returns a special case object.

### 6. Don't Pass Null
- Unless you are working with an API which expects you to pass null, you should avoid passing null in your code whenever possible.