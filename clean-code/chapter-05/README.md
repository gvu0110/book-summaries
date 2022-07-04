# Chapter05
## Formatting

### 1. Vertical Formatting
**The Newspaper Metaphor**
- We would like a source file to be like a newspaper article.
- The name should be simple but explanatory.
- The topmost parts of the source file should provide the high-level concepts and algorithms. - Detail should increase as we move downward, until at the end we find the lowest level functions and details in the source file.

**Vertical Openness Between Concepts**
- Should be there are a blank lines that separate the package declaration, the import(s), and each of the functions as the following:
```java
package fitnesse.wikitext.widgets;

import java.util.regex.*;

public class BoldWidget extends ParentWidget {
    public static final String REGEXP = "'''.+?'''";
    private static final Pattern pattern = Pattern.compile("'''(.+?)'''",
        Pattern.MULTILINE + Pattern.DOTALL
    );

    public BoldWidget(ParentWidget parent, String text) throws Exception {
        super(parent);
        Matcher match = pattern.matcher(text);
        match.find();
        addChildWidgets(match.group(1));
    }

    public String render() throws Exception {
        StringBuffer html = new StringBuffer("<b>");
        html.append(childHtml()).append("</b>");
        return html.toString();
    }
}
```
**Vertical Density**
- The lines of code that are more related to each other should appear close to each other.

**Vertical Distance**
- ***Variable Declarations***:
    + Variables should be declared as close to their usage as possible.
    + Local variables should appear at the top of each function.
    + Loops-control variables should usually be declared within the loop statement.
    + In rare cases, a variable might be declared at the top of a block or just before a loop in the long function.
- ***Instance Variables***:
    + Should be declared in one well-known place (at the top of the class).
- ***Dependent Functions***:
    + If one function calls another, they should be vertically close, and the caller should be above the callee.
- ***Conceptual Affinity***:
    + Certain parts of code want to be near other parts, sometimes because a group of functions perform a similar operation or share a common naming scheme.

**Vertical Ordering**
- A function that is called should be below a function that does the calling.
- It creates a nice flow down the source code module from high level to low level.

### 2. Horizontal Formatting
How wide should a line be? The best answer for that is **"you should never have to scroll to the right"**. **"I personally set my limit at 120 characters per line"** - Uncle bob said.

**Horizontal Openness and Density**
- We didn't put horizontal space for things that are more related, and we put horizontal space for things are less related (are separate).
- For example, don't put spaces between the function names and the `(`.
- Separate arguments within the function call by `, ` to show that the arguments are separate.
```java
private void measureLine(String line) {
    lineCount++;
    int lineSize = line.length();
    totalChars += lineSize;
    lineWidthHistogram.addLine(lineSize, lineCount);
    recordWidestLine(lineSize);
}
```
- The factors have no horizontal space between them because they are high precedence.
- The terms are separated by horizontal space because `+` and `-` are lower precedence.
```java
private static double determinant(double a, double b, double c) {
    return b*b - 4*a*c;
}
```
**Horizontal Alignment**
- Avoid the horizontal alignment because it leads eyes away from the true purpose, like the following example:
```java
public FitNesseExpediter(Socket s, FitNesseContext context) throws Exception {
    this.context            = context;
    socket                  = s;
    input                   = s.getInputStream();
    output                  = s.getOutputStream();
    requestParsingTimeLimit = 10000;
}
```
**Indentation**
- Statements at the level of the file, such as class declarations, are not indented
- Methods within a class are indented one level to the right of the class.
- Implementations of those methods are indented one level to the right of the method declaration.
- Block implementations are implemented one level to the right of their containing block, and so on.

### 3. Team Rules
A team of developers should agree upon a single formatting style, and then every member of that team should use that style.