# Clean Code
Notes on the book Clean Code - A Handbook of Agile Software Craftsmanship by Robert C. Martin

# Index

[Foreword](#foreword)

[Introduction](#introduction)

1. [Clean Code](#clean-code)
2. [Meaningful Names](#meaningful-names)
3. [Functions](#functions)
4. [Comments](#comments)
5. [Formatting](#formatting) 
6. [Objects and Data Structures](#objects-and-data-structures) 
7. [Error Handling](#error-handling) 
8. [Boundaries](#boundaries) 
9. [Unit Tests](#unit-tests)
10. [Classes](#classes) 
11. [Systems](#systems) 
12. [Emergence](#emergence)
13. [Concurrency](#concurrency)
14. [Successive Reﬁnement](#successive-refinement) 
15. [JUnit Internals](#junit-internals) 
16. [Refactoring SerialDate](#refactoring-serialdate) 
17. [Smells and Heuristics](#smells-and-heuristics) 

# <a name="foreword">Foreword</a>
Small things matter. God is in the details.

80% or more of what we do is quaintly called "maintenance": the act or repair.

They introduce us the concept of Total Productive Maintenance (TMP) (1951 from the Japaneses):
* **Seiri**: Knowing where things are: naming is crucial.
* **Seiton**: A piece of code should be where you expect to find it.
* **Seiso**: Keep the workplace free of unuseful things (comments, etc).
* **Seiketsu**: Standardization. The group agrees about how to keep the workplace clean.
* **Shutsuke**: Discipline. Follow the practices.

You should name a variable using the same care with which you name a first-born child.

They talk about that they found significant indicators that code with consistent indentation style had lower bug density than code with bad indentation.

Try to do the best to leave the campground cleaner than you find it.

The code is the design and Simple Code are their mantras.

In Scrum make refactoring part of your concept of done.

Be honest about the state of your code because code is never perfect.

# <a name="introduction">Introduction</a>
Measurement of code Quality: WTFs/Minute.

Customers leaving in droves and managers breathing down our necks... Craftsmanship is the answer.

Learning to write clean code is hard work. You must practice it yourself.

# <a name="clean-code">1. Clean Code</a>
## There Will Be Code
Nonsense: Programmers won't be needed because business people will generate programs from specifications.

The level of abstraction of our programing languages will increase but there will be code.

Well specified requirements can act as executable tests for our code.

## Bad Code

Bad code can bring a company down.

There are no excuses for bad code, no reasons: your boss does not give you time, you want to finish faster to get more backlog's stories finished...

I will clean it later... **Later equals never**.

## The Total Cost of Owning a Mess
It will drive the productivity ever further toward zero.
## The Grand Redesign in the Sky
If you decide to redesign your system, with a different team, maybe you will get:
* Two teams in a race
* Years of development are necessary to provide the same features
* People will leave the company and the redesign becomes a messy for newer members and they want to redesign it again...
## Attitude
Why does this happen to code? requirements?, stupid managers?, schedules ?? **No**.

It is all about unprofessionalism.

Most managers want good code. We have to help them to understand the risks of bad code.
## The Primal Conundrum
The only way to go fast is to get the code as clean as possible.
## The Art of Clean Code?
Writing clean code require discipline. We need to work hard to get "code-sense".
## What Is Clean Code?
* Broken windows concept: looks like nobody cares about it
* Code without test is not clean.
* Clean code always looks like it was written by someone who cares.
* **No duplication, one thing, expressiveness, tiny abstractions**.
* It does pretty much as you expected: obvious, simple and compelling
## Schools of Thought
## We Are Authors
* *@author* tells as who we are.
* To write new code we need to read the old one.
* The ratio of time spent reading vs writing is 10:1.
## The Boy Scout Rule
**Leave the campground cleaner than you found it**.

The clean up does not have to be something big.
## Prequel and Principles
## Conclusion
## Bibliography

# <a name="meaningful-names">2. Meaningful Names</a>
## Introduction
Names are everywhere in software: variables, functions, args, classes, packages, files...
## Use Intention-Revealing Names
The name should answer all the big questions:
* Why it exists?
* What it does? 
* How it is used?

Avoid use this like:
```java
int d; // elapsed time in days
```
Instead of that use a name that specifies what is being measured and his unit:
```java
int elapsedTimeInDays;
```
Choosing names that reveal intent can make it much easier to understand and change code. This is helpful to others as well as your future self. What is the purpose of this code?

From this:
```java
public List<int[]> getThem() {
	List<int[]> list1 = new ArrayList<int[]>();
	for (int[] x : theList)
		if (x[0] == 4)
			list1.add(x);
	return list1;
}
```
We can improve it only with revealing naming:

```java
public List<int[]> getFlaggedCells() {
	List<int[]> flaggedCells = new ArrayList<int[]>();
	for (int[] cell : gameBoard)
		if (cell[STATUS_VALUE] == FLAGGED)
			flaggedCells.add(cell);
	return flaggedCells;
}
```
And it is still better with a Cell class:

```java
public List<Cell> getFlaggedCells() {
	List<Cell> flaggedCells = new ArrayList<Cell>();
	for (Cell cell : gameBoard)
		if (cell.isFlagged())
			flaggedCells.add(cell);
	return flaggedCells;
}
```
## Avoid Disinformation 
If you want to name a group of accounts use **accounts** try to avoid *accountList* (maybe its type is not a List)

Beware of using names that are very similar *XYZFooBarClassForBlabla* and *XYZFooBarClassForBlablable*

Using lower case *l* (looks like 1) and uppercase *O* (looks like 0) are also unhelpful.
## Make Meaningful Distinctions 

Do not use number-series naming: a1, a2, ... aN

```java
public static void copyChars(char a1[], char a2[]) {
	for (int i = 0; i < a1.length; i++) {
		a2[i] = a1[i];
	}
}
```
This would be much better with **source** and **destination** as argument names.

Avoid Noise words (Info, Data, a, an, the, variable, table, String): 
* ProductInfo and ProductData are more or less the same.
* Is nameString better than name? No.

The same for methods, what I should do?: 
getActiveAccount() getActiveAccounts() getActiveAccountInfo()

## Use Pronounceable Names
If you can't pronounce it you can't discuss it without sounding like an idiot. Example:
```java
// generation date, year, months, day, hour, minute, and second
class DtaRcrd102 {
	private Date genymdhms;
	/* ... */
}

// better:
class Customer {
	private Date generationTimestamp;
	/* ... */
}
```
## Use Searchable Names 
Single letter names and numeric constants are not easy to locate across a body of text.
i.e.:
```java
for (int j=0; j<34; j++) {
	s += (t[j]*4)/5;
}
```
It's better when has searchable names:
```java
int realDaysPerIdealDay = 4;
const int WORK_DAYS_PER_WEEK = 5;
int sum = 0;
for (int j=0; j < NUMBER_OF_TASKS; j++) {
	int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
	int realTaskWeeks = (realdays / WORK_DAYS_PER_WEEK);
	sum += realTaskWeeks;
}
```
## Avoid Encodings 

Don't use symbols, emojis.
## Hungarian Notation, Member Preﬁxes

Old examples from Fortran, BASIC. No longer likely to be applicable.
## Interfaces and Implementations 
Leave interfaces unadorned:

*ShapeFactory* and *ShapeFactoryImp* are better than *IShapeFactory* and *ShapeFactory*
## Avoid Mental Mapping 
Just because you *can* remember that `this` means `that` doesn't mean you should write your code that way.
> One difference between a smart programmer and a professional programmer is that the professional understands *clarity is king*. Professionals use their powers for good and write code that others can understand.
## Class Names 
A class name should be a **noun**, not a verb. Avoid words like Manager, Processor, Data, or Info.
Good names could be: Customer, WikiPage, Account, AddressParser.
## Method Names
Methods should have verb or verb phrase names like postPayment, deletePage, save...

When constructors are overloaded use static factory methods with names that describe the arguments:
```java
Complex fulcrumPoint = Complex.FromRealNumber(23.0);
```
better than
```java
Complex fulcrumPoint = new Complex(23.0);
```
## Don’t Be Cute 
Don't use slang!: whack() instead of kill()

**Say what you mean. Mean what you say.**
## Pick One Word per Concept
If you choose *get()* use it always (instead of fetch, retrieve, etc.)
## Don’t Pun 
Avoid using the same word for two purposes (*add()* method could mean different things in different classes...)

**Make your code as easy as possible to understand.**
## Use Solution Domain Names 
Use pattern names: Factory, Visitor, Decorator, etc. The people who read your code will be programmers so if there is a commonly understood term, it's ok to use it.
## Use Problem Domain Names
And you could ask a domain expert if you have doubts when there is no 'programmer way' to define something. I.e. the term you use is familiar to people in the project, company, etc.
## Add Meaningful Context 
Variables usually don't have a mean by themselves. You will need a context.

Names like: firstName, lastName, street, postalCode, etc. Are names from an address.

If you have problems with context you can add a prefix: addrFirstName, addrLastName, etc.

But It would be better if you put them into a class Address => you will have a great context.

When a method has a lot of variables with an unclear context you can try to break it into smaller functions.

## Don’t Add Gratuitous Context 
Don't use prefix in all your classes/methods to say that they belongs to an specific context.
Gas Station Deluxe => GSD and then you have: GSDAccountAddress... it is not a good name.

**Shorter names are generally better than longer ones**.

## Final Words 
Follow these rules and refactor code to help resolve these problems.

# <a name="functions">3. Functions</a>
Functions are the first line of organization in any program.
## Small!
First: they should be small. Second: they should be smaller than that.

* Functions should hardly ever be **20 lines long**.
* Functions should be **transparently obvious**.
* Each function tells a story.
* Each function leads you to a next thing in a compelling order.

## Blocks and Indenting

The blocks within *if*, *else*, *while*, etc. statements should be one line long, probably will be a function call.

This function call can have a nice and descriptive name

The indent level of a function should not be greater than one or two.

## Do One Thing

```
FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL. THEY SHOULD DO IT ONLY
```

A function do one thing though it contains calls to other functions. But those functions should be always one level below to the stated name of the function.

We create functions to decompose a larger concept (the name of the function) into a set of steps at the next level of abstraction.

## Sections within Functions 
**A function that is divided into section will be probably doing more than one thing.**

## One Level of Abstraction per Function 
Don't mix levels of abstraction in a function. It gets harder to tell whether a particular expression is important of a small detail.

## Reading Code from Top to Bottom: The Stepdown Rule
Write code like a top-down set of TO-paragraphs where each paragraph provides further instructions on the one before it. TO build the page we include setups then include the test page. TO include setups we include the suite setup if this is a suite. TO include the suite setup...

## Switch Statements 
Switch statements always do N things.

Use them to create polymorphic objects. Abstract Factory pattern.

## Use Descriptive Names
You know that you are working with clean code when each routine turns out to be pretty much as you expected.

Use descriptive names. A long descriptive name is better than a short enigmatic one, and better than a long descriptive comment.

Be consistent with your names, try always to use the same verbs, nouns, etc.

*includeSetupAndTeardownPages, includeSetupPages, includeSetupPage...*

## Function Arguments
* Zero arguments (niladic)
* One argument (monadic)
* Two arguments (dydadic)
* ~~Three arguments (triadic)~~
* ~~Four arguments~~
* ..

Zero arguments > One argument > Two arguments

**Avoid output arguments**, they are not easy to understand.

## Common Monadic Forms
* Asking a question about that argument.*boolean fileExists("miFile")*
* Operating on that argument, transforming and returning *InputStream fileOpen("miFile")*
* Events to alter the state of the system.

Try to avoid other forms.

## Flag Arguments 
Flag arguments (true|false) are ugly. Functions with that do one thing if it is true and another thing if is false.

Split the function in two:
*render(boolean isSuite) => renderForSuite() , renderForSingleTest()*

## Dyadic Functions
They are harder to understand than monadic functions.
*assertEquals(expected, actual)* ... it would take practice to remember which order to put the arguments in.

## Triads
The are harder to understand than dyadic functions.
*assertEquals(msg, expected, actual)* ... now the msg seems to be the expected value.

## Argument Objects
When a function needs to have more than two or three arguments some of these argument should be wrapped into a class of their own.
*makeCircle(double x, double y, double radius) =>  makeCircle(Point center, double radius);*

## Argument Lists 
Function that takes argument lists can be monads, dyads or even triads:
*void monad(String... args); void dyad(String name, String... args); void triad(String name, int count, String... args)*

## Verbs and Keywords
We can encode the name of the arguments into the function name:
*assertEquals => assertExpectedEqualsActual*

And we can do more meaning to the argument:
*write(name) => writeField(name)*

## Have No Side Effects 
Functions should not do things that you don't expect.
i.e: checkPassword(login, password) => inside initializes the user session...initializing the user session should be its own function.

## Output Arguments 
The should be avoided with OOP. If you see `appendFooter(s)`, is `s` being appended to something, or are you appending something to `s`?
*void appendFooter(StringBuffer report); => report.appendFooter();*

## Command Query Separation 
Functions should either do something or answer something, but not both.
*attributeExists and setAttribute* should be different functions. Avoid things like *setAndCheckIfExists*

## Prefer Exceptions to Returning Error Codes 
Error codes violate Command Query Separation.

Exceptions can help to separate the happy path code from the error path and that helps to simplificate.

## Extract Try/Catch Blocks 
Try/catch's are ugly. It is better to extract try and catch methods.

## Error Handling Is One Thing
Methods with try/catch should only have this structure and nothing more.

## The Error.java Dependency Magnet 
Error codes are usually in classes like Error.java (with constants). Avoid that, it is a dependency magnet (it is everywhere) and nobody wants to add new errors or change it because you have to recompile/deploy everything. Instead the tendency will be to re-use error codes for uses they aren't intended for.

Use Exceptions instead of Error codes.

## Don’t Repeat Yourself 
Duplication may be the root of all evil in software.

## Structured Programming 
Things like "there should only be one return statement" is unnecessary when you create small functions.

## How Do You Write Functions Like This? 
* Write ugly and long functions with a long list of arguments
* You need to have unit tests that cover all that functions.
* Then you can to massage and refine that code. You can break everything in classes and keep your test passing.

## Conclusion
Functions are the verbs and classes are the nouns of the language of our system.

Your real goal is to tell the story of the System. You have to write functions that help you to tell that story.



# <a name="comments">4. Comments</a>
If we were expressive enough in our programming language we would not need comments.

Comments are always failures. **Express yourself in code instead!**

Code changes and evolves...the comments don't always get moved or updated with code changes!

## Comments Do Not Make Up for Bad Code
"Ooh, I would better comment that!" => No! You would be better clean it!

## Explain Yourself in Code 
This:
```java
// Check to see if the employee is eligible for full benefits
if (employee.flags && HOURLY_FLAG) && (employee.age >65)) {
```
vs:
```java
// Check to see if the employee is eligible for full benefits
if (employee.isEligibleForFullBenefits()){
```
=> **Create a function that says the same thing as the comment you want to write**

## Good Comments
The only truly good comment is the comment you found a way not to write.

### Legal Comments
Put all the terms and conditions into an external document.

### Informative Comments
Useful information about the implementation and taken decisions.

### Explanation of Intent
Take care that there is no better way, and then take even more care that they are accurate.

### Clariﬁcation
If you do it take care that there is no better way and the are accurate.

### Warning of Consequences 
Warn other programmers about certain consequences:
- Maybe a test that lasts a lot => try to use @Ignore
- Something that is not thread safe and you have to use "new" each time.

### TODO Comments
It is not an excuse to leave bad code in the system.

You do not want your code to be littered with TODOS => san them regularly and eliminate the ones you can.

### Ampliﬁcation
If something is very very important you can amplify it.

### Javadocs in Public APIs
If you are writing a public API => write good docs for it. (but they can lie as any other kind of comment).

## Bad Comments 
Most comments fall into this category.

### Mumbling 
A catch block empty with a comment => was the author trying to tell himself to come later to do it?

Any comment that forces you to look in another module to know the meaning is wrong.

### Redundant Comments 
* Less information than the code.
* It is not easier to read than the code.
* It is less precise

### Misleading Comments

### Mandated Comments
**A rule that says that every function/property/variable must have a javadoc is stupid**

You will finally get things like: @param author The author

### Journal Comments
We have source control now => they should be completely removed.

### Noise Comments 
Auto generated or very obvious comments that are nothing but noise.

### Scary Noise 
Maybe with copy/paste errores... are they a bug?

### Don’t Use a Comment When You Can Use a Function or a Variable
Consider the following stretch of code:

```java
// does the module from the global list <mod> depend on the
// subsystem we are part of?
if (smodule.getDependSubsystems().contains(subSysMod.getSubSystem()))
```
This could be rephrased without the comment as
```java
ArrayList moduleDependees = smodule.getDependSubsystems();
String ourSubSystem = subSysMod.getSubSystem();
if (moduleDependees.contains(ourSubSystem))
```
### Position Markers
Things like:
```java
// Actions ////////////////////////////////////////////////
```
Noise, obvious and usually ignored... do not use banners
### Closing Brace Comments
Might leave a comment to mark which braces close which part of the function. Better to write shorter functions without so much nesting.
### Attributions and Bylines
Added by:... SCM's are a better place for this.
### Commented-Out Code
Trust in SCM's... **delete the code**.
### HTML Comments 
HTML in source code comments is an abomination: it makes them really hard to read.
### Nonlocal Information 
The comment should describe the code it appears near.
### Too Much Information 
### Inobvious Connection
Maybe the comment needs its own explanation...
### Function Headers
Short functions do not need much description. We prefer well-chosen names than a comment header.


# <a name="formatting">5. Formatting</a>
We want people to perceive that professionals have been at work... not to see a scrambled mass of code that looks like it was written by a bevy of drunken sailors.

**You should take care your code is nicely formatted**

In a team: define a single set of formatting rules that everybody should comply.
## The Purpose of Formatting 
Code formatting is about communication.

Readability of code.
## Vertical Formatting 
Small files are easier to understand than large files.

It is possible to build significand system(junit, tomcat, ant, fitnesse) with files between **200-500 lines.**
## The Newspaper Metaphor 
**We would like a source file to be like a newspaper article**:
- At the top you expect a headline
- The first paragraph gives you a synopsis of the whole story.
- As you continue downward the details increase

In a source file: 
high-level concepts and algorithms => lowest level functions and details

## Vertical Openness Between Concepts 
* line => expression or clause.
* group of lines => complete thought.
* thoughts are separated with blank lines.

## Vertical Density 
Useless comments in class's properties make the class more difficult to read it. Example
```java
public class ReporterConfig {
 /**
 * The class name of the reporter listener
 */
 private String m_className;
 /**
 * The properties of the reporter listener
 */
 private List<Property> m_properties = new ArrayList<Property>();

 public void addProperty(Property property) {
   m_properties.add(property);
}
```
vs

```java
public class ReporterConfig {
 private String m_className;
 private List<Property> m_properties = new ArrayList<Property>();

 public void addProperty(Property property) {
   m_properties.add(property);
}
```
## Vertical Distance 
### Variable declaration:
**Variables should be declared as close to their usage as possible**
Our functions are short -> local variables at the top.
Control variables for loops => declare them within the loop statement
### Instance variables
Should be declared at the top of the class.
Everybody should know where to go to see the declarations.
### Dependent functions
If one functions calls another they should be vertically close, an the caller should be above the callee, if it is possible.
### Conceptual Affinity
Group of functions performing a similar operation.
They share common naming scheme and perform variations of the same task. We want them to be close together.
## Vertical Ordering 
Downward direction => flow from high level to low level
## Horizontal Formatting
Programmers clearly prefer short lines.
**Keep your lines short!**
**Limit 120 characters**
You should never have to scroll to the right
## Horizontal Openness and Density 
We use white spaces in:
* Operators to accentuate them.
* Arguments in function calls and definitions (after the comma).

Don't put white spaces between function's name and the opening parenthesis => They are closely related

Example:
```java
public class Quadratic {
 public static double root1(double a, double b, double c) {
   double determinant = determinant(a, b, c);
   return (-b + Math.sqrt(determinant)) / (2*a);
 }

 public static double root2(int a, int b, int c) {
   double determinant = determinant(a, b, c);
   return (-b - Math.sqrt(determinant)) / (2*a);
 }

 private static double determinant(double a, double b, double c) {
  return b*b - 4*a*c;
 }
}
```
## Horizontal Alignment
Horizontal alignment is not useful:
* You read down the list of variable names without looking a their types.
* You look down the list of rvalues without ever seeing the assignment operator.
* Automatic reformatting tools usually eliminate it.
Example:
```java
public class FitNesseExpediter implements ResponseSender
{
  private    Socket        socket;
  private    InputStrea    input;

  public FitNesseExpediter(Socket          s,
                           FitNesseContext context) throws Exception
  {
    this.context = context;
    input =        s.getInputStream();
  }
}
``` 
vs
```java
public class FitNesseExpediter implements ResponseSender
{
  private Socket socket;
  private InputStream input;

  public FitNesseExpediter(Socket s, FitNesseContext context) throws Exception {
    this.context = context;
    input = s.getInputStream();
  }
}

``` 
## Indentation
**Without indentation programs would be virtually unreadable by humans**

Try to avoid breaking rules collapsing everything in one line with short if's, loops, functions.

## Dummy Scopes
If the body of a while/for is a dummy make the body indented and surrounded by braces.

## Team Rules
**Every programmer has his own favorite formatting rules, but if he works in a team, them the team rules**

# <a name="objects-and-data-structures">6. Objects and Data Structures</a>
We keep our variables private. Nobody depends on them. Freedom to change their type or implementation. If you don't need them don't expose the with public getters an setters!
## Data Abstraction
Hiding implementation is about abstractions. 

A class does not simply push its variables out through getters and setters. Rather it exposes abstract interfaces that allow its users to manipulate the essence of the data, without having to know its implementation.

Concrete Point
```java
public class Point {
 public double x;
 public double y;
}
```
Abstract Point
```java
public interface Point {
 double getX();
 double getY();
 void setCartesian(double x, double y);
 double getR();
 double getTheta();
 void setPolar(double r, double theta);
}
```
Abstract point it's hiding its implementation. The methods enforce an access policy => read coordinates independently but write them together.

Concrete Vehicle
```java
public interface Vehicle {
 double getFuelTankCapacityInGallons();
 double getGallonsOfGasoline();
}
```
Abstract Vehicle
```java
public interface Vehicle {
 double getPercentFuelRemaining();
}
```
Abstract vehicle doesn't expose the details of the data.

**The worst option is to blithely add getters and setters**
## Data/Object Anti-Symmetry 
**Objects** vs **Data structures**
* Objects hide their data behind abstractions and expose functions that operate on that data.
* Data structures expose their data and have no meaningful functions.

**OO code** vs **Procedural code**
* OO code makes it easy to add new classes without changing existing functions
* Procedural code makes it easy to add new functions without changing the existing data structures.
* OO code makes hard to add new functions because all the classes must change.
* Procedural code makes it hard to add new data structures because all the functions must change.

**Sometimes you need data structures and sometimes you need objects!**
## The Law of Demeter
**talk to friends, not to strangers**

A method *f* of a class *C* should only call methods of these:
* C
* An object created by *f*
* An object passed as an argument to *f*
* An object held in an instance variable of *C*

Avoid this (called train wreck):
```java
final String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath();
```
Try to split them:
```java
Options opts = ctxt.getOptions();
File scratchDir = opts.getScratchDir();
final String outputDir = scratchDir.getAbsolutePath();
```
### Train Wrecks 
=> bunch of coupled train cars!
Is this a violation of Demeter's Law? it depends...
* if context, options and scratchDir are objects is a clear violation of the Law.
* if they are data structures with no behavior Demeter's Law does not apply.

If it was a data structure you could use it this way:
```java
final String outputDir = ctxt.options.scratchDir.absolutePath;
```
### Hybrids 
Public fields + methods => Avoid creating them. Worst of both words: hard to add new functions and hard to add new data structures.

### Hiding Structure 
You could think in these options:
```java
ctxt.getAbsolutePathOfScratchDirectoryOption();
```
=> explosion of methods in ctxt object
or
```java
ctx.getScratchDirectoryOption().getAbsolutePath()
```
=> it returns a data structure, not an object.

Neither options fells good.

**You tell an object to do something you should not be asking it about its internals**
Why do you want to know the absolute path?.. to create something:

```java
BufferedOutputStream bos = ctxt.createScratchFileStream(classFileName);
```
=> ctx hide its internals and we are not violating Demeters' Law.
### Data Transfer Objects
Structures to communicate with databases, parsing messages from sockets...

You usually use Beans => private properties with setters and getters. It is ok for OO purist but no other benefits. 
### Active Record
**Data structures** with public (or beans) properties and methods like save, find, etc.

Developers put business logic in them => Error!

## Conclusion
Choose the right approach!
* Flexibility to add new data types => objects
* Flexibility to add new behaviors => data types and procedures


# <a name="error-handling">7. Error Handling</a>
Things can go wrong, we as programmers are responsible for making sure that our codes does what it needs to do => **and should be clear!**

Error handling is important but if it obscures logic it's wrong.
## Use Exceptions Rather Than Return Codes 
It is better to throw an exception.
* The calling code is cleaner.
* Its logic is not obscured by error handling.

Try to separate the algorithm from error handling:
```java
public void sendShutDown() {
  try {
    tryToShutDown();
  } catch (DeviceShutDownError e) {
    logger.log(e);
}
private void tryToShutDown() throws DeviceShutDownError {
  // ..
}
```
## Write Your Try-Catch-Finally Statement First 
Try blocks are like transactions => *catch* has to leave your program in a consistent state, no matter what happens in the try.

Write test that force exceptions and add behavior to satisfy your test.

## Use Unchecked Exceptions 
Your code would not compile if the signature don't match to what your code do.

Some programing languages do not have it and you can build robust software with them.

Declaring the exception between you and *the catch* is a Open/Close Principle violation => a change at a low level can force changes on many higher levels.

Encapsulation is broken because all functions in the path of a throw must know about details of that low-level exception.

## Provide Context with Exceptions
Pass enough information to be able to log the error in the catch. A stack trace won't tell you the *intent* of the operation that failed.

## Deﬁne Exception Classes in Terms of a Caller’s Needs
Sometimes is very useful to write a simple wrapper that catches an translates exceptions from a third-party API => minimize the dependencies upon it and you can move to other different library without much penalty.

## Deﬁne the Normal Flow 
SPECIAL CASE PATTERN [Fowler]: you create a class or configure an object so that it handles a special case for you => the client code does not have to deal with exceptional behavior because is encapsulated. 

Example:
```java
try {
  MealExpenses expenses = expenseReportDAO.getMeals(employee.getID());
  m_total += expenses.getTotal();
} catch(MealExpensesNotFound e) {
  m_total += getMealPerDiem();
}
```
vs:
```java
MealExpenses expenses = expenseReportDAO.getMeals(employee.getID());
m_total += expenses.getTotal();
// the Exception is handled in the DAO and getMails returns
// PerDiemMealExpenses if an error is thrown...
public class PerDiemMealExpenses implements MealExpenses {
 public int getTotal() {
 // return the per diem default
 }
}

```
## Don’t Return Null
If you return null then you have to manage "the null" with if's...".

When we return null we are creating work for ourselves.

You can return an empty list and clean up the code:

```java
List<Employee> employees = getEmployees();
if (employees != null) {
  for(Employee e : employees) {
    totalPay += e.getPay();
  }
}
```
vs
```java
List<Employee> employees = getEmployees();
for(Employee e : employees) {
  totalPay += e.getPay();
}
//...
public List<Employee> getEmployees() {
  if( .. there are no employees .. )
     return Collections.emptyList();
}
```
## Don’t Pass Null 
**Returning null from methods is bad, but passing null into methods is worse**

You have to deal with null, with if's or with assertions at the beginning asserts are good documentation).

A null in an argument is an indication of a problem.
## Conclusion
Clean code is readable, but it must also be robust! These are not conflicting goals: error handling can be seen as a separate concern, independent of the main logic.


# <a name="boundaries">8. Boundaries</a>

How to integrate code with 3rd-party or open source software.

## Using Third-Party Code
Natural tension between provider/user of an interface. **Provider** => focus on wide audience.  **User** => focus on their particular needs.

Example: java.util.Map
Map is an interface with a lot of methods: clear, containsKey, containsValue, get, isEmpty, put, putAll, remove, size...
It is very flexible, any user can add items of any type to nay Map.

If we need a Map of Sensors you can create something like:
```java
// Without generics
Map sensors = new HashMap();
Sensor s = (Sensor) sensors.get(sensorId);
// With generics:
Map<Sensor> sensors = new HashMap<Sensor>();
Sensor s = sensors.get(sensorId);
```
This is not clean code. If you use instances of Map<Sensor> in your system if the Map Interface changes you will have to change a lot of references.

Try to encapsulate any boundary interface like Map inside a the class:
```java
public class Sensor {
  private Map sensors = new HashMap();

  public Sensor getById(String id) {
    return (Sensor) sensor.get(id);
  }

}
```
Avoid returning it or accepting it as an argument in public APIs.

## Exploring and Learning Boundaries
**Learning tests** instead of experimenting an trying out the new stuff in our production code, we could write some tests to explore our understanding of the third-party code. 
 
## Learning Tests Are Better Than Free
Since you have to learn the 3rd party code anyway, learning tests are an easy way to learn *and* future-proof use of the API. With each release comes a new risk => we run the learning tests to see the changes.

Without these tests the migration is easier, without them we could stay with the old version longer than we should.
## Using Code That Does Not Yet Exist
Sometimes you have boundaries in your system that represents things that had not been designed yet.

You can create your own interface with the idea of how this should work and implement a Fake implementation for testing purposes.
See the Adapter pattern.
## Clean Boundaries 
When we use code that is out of our control special care must be taken to protect our investment and make sure future change is not too costly.

Wrap them or use an Adapter to convert from our perfect interface to the provided interface.

# <a name="unit-tests">9. Unit Tests</a>
The Agile and TDD movements have encouraged many programmers to write unit tests but many of them have missed important points of writing good tests.

## The Three Laws of TDD 
* **First Law**: You may not write production code until you have written a failing unit test.
* **Second Law**: You may not write more of a unit test than is sufficient to fail, and not compiling is failing.
* **Third Law**: You may not write more production code than is sufficient to pass the currently failing test.

If we follow these rules we will write dozens of tests per day, hundreds of tests per month and thousands of tests every year. These tests can rival the size of the production code and can present a daunting management problem.

## Keeping Tests Clean 
Dirty tests are equivalent or worse than having no tests! Need to follow the same rules of well-named variables, short & descriptive functions.

Book example story: When managers asked why their estimates were getting so large, the developers blamed the tests. In the end they were forced to discard the test suite entirely.

But without a test suite:
* We lost the ability to make sure that changes work as expected and do not break other parts of our system.
* We start to fear making changes.
* We stop cleaning our production code => more harm than good.
* => bugs, frustrated customers, the feeling that our testing effort had failed.

**Test code is just as important as production code, its not a second-class citizen**. It requires thought, design and care. Keep it as clean as production code.
## Tests Enable the -ilities

**If you don't keep your test clean, you will lose them**

Unit tests keep our code flexible, maintainable and reusable. Without them every change is a possible bug.

You can improve that architecture and design without fear!

## Clean Tests 
**Readability makes clean test.**
Clarity, simplicity and density of expression => say a lot with a few expressions as possible.

The test code must be designed to be read.

Example

Without refactor:
```java
public void testGetPageHieratchyAsXml() throws Exception
{
	crawler.addPage(root, PathParser.parse("PageOne"));
	crawler.addPage(root, PathParser.parse("PageOne.ChildOne"));
	crawler.addPage(root, PathParser.parse("PageTwo"));

	request.setResource("root");
	request.addInput("type", "pages");
	Responder responder = new SerializedPageResponder();
	SimpleResponse response =
		(SimpleResponse) responder.makeResponse(
				new FitNesseContext(root), request);
	String xml = response.getContent();

	assertEquals("text/xml", response.getContentType());
	assertSubString("<name>PageOne</name>", xml);
	assertSubString("<name>PageTwo</name>", xml);
	assertSubString("<name>ChildOne</name>", xml);
}
```

Refactored:
```java
public void testGetPageHierarchyAsXml() throws Exception {
	makePages("PageOne", "PageOne.ChildOne", "PageTwo");

	submitRequest("root", "type:pages");

	assertResponseIsXML();
	assertResponseContains(
			"<name>PageOne</name>", "<name>PageTwo</name>", "<name>ChildOne</name>"
	);
}
```

**BUILD-OPERATE-CHECK** pattern:
* Build: the first part builds up the test data.
* Operate: the second part operates on that test data.
* Check: the third part checks that the operation yielded the expected results

You can read the test very quickly without being overwhelmed by details.

## Domain-Speciﬁc Testing Language
Functions and utilities that make the test more convenient to write and easier to read.

It requires a continued refactoring.

## A Dual Standard 
The code within the testing API will be simple, succint, expressive but it need not be as efficient as production code. It runs in a test environment and it has different needs.

You can write code that may break rules or is not very efficient but is ok if it makes the test easy to understand.

Dual standard: There are things that you might never do in a production environment that are perfectly fine in a test environment.

## One Assert per Test 
This is a good guideline but the best thing we can say is that **the number of asserts in a test should be minimized.**

## Single Concept per Test 
Better than one assert per test.

**Best rule:** 
* **You should minimize the number of asserts per concept and test just one concept per test function**

## F.I.R.S.T
* **Fast**: you want to run them fequently.
* **Independent**: should not depend on each other.
* **Repeatable**: in any environment, in your laptop, without network...
* **Self-Validating**: should have a boolean output... not a log that you have to read to know the result.
* **Timely**: Write them before the production code, if you do it after maybe the production code will be hard to test.

## Conclusion
**If you let the test rot, then your code will rot too. Keep your test clean!**


# <a name="classes">10. Classes</a>

Classes belong to higher levels of code organization.
## Class Organization 
Like a newspapaer article:
* public static constants
* private static variables
* private instance variables
* public functions
* private functions

## Encapsulation 
Utitlity functions should be private but could be protected to be accesible by tests in the same package.

## Classes Should Be Small!
... and then should be smaller than that!.

With functions we count lines, with classes we count responsibilities.

Too many responsibilities => God class.

Avoid to include words like 'Processor, Manager, Super' in classnames => aggregation of responsibilities.

Class **description in 25 words** without "if", "and", "or", "but"...

## The Single Responsibility Principle
**Classes should have one responsibility**--**one reason to change**.

Too many of us think that we are done once the program works. We move on the next problem rather than going back and breaking the classes into decoupled units with single responsibilities.

We have to organize system complexity. A developer should know where to llok to find things and need only understand the directly affected complexity at any given time.

We want systems composed of many small classes. Single responsibility and single reason to change. They colaborate with a few others to achieve the desired system behavior.

## Cohesion
Small number of instance variables => each method manipulates one or more of those variables. => more variables manipulate => more cohesive a method is.

A class in wich each variable is used by each method is maximally cohesive.

## Maintaining Cohesion Results in Many Small Classes
When classes lose cohesion split them!

Breaking a large function into many smaller functions often gives us the opportunity to split several smaller classes out as well => better organization and more transparent structure.

Do it with tests => write a test suit that verified the precise behavior of the first version. Then tiny little changes, one at a time to get the desired result.
## Organizing for Change 
**Open-Closed Principle** => Our classes should be open for extension but closed for modification.

Allow new functionality via subclassing.

We incorporate new features by extending the system, not by making modifications to existing code.
## Isolating from Change
**Dependency Inversion Principle (DIP)** => Classes should depend upon abstractions, not on concrete details.
## Bibliography

# <a name="systems">11. Systems</a>
## How Would You Build a City? 
## Separate Constructing a System from Using It 
## Separation of Main 
## Factories 
## Dependency Injection
## Scaling Up 
## Cross-Cutting Concerns 
## Java Proxies
## Pure Java AOP Frameworks
## AspectJ Aspects 
## Test Drive the System Architecture
## Optimize Decision Making 
## Use Standards Wisely, When They Add Demonstrable Value
## Systems Need Domain-Speciﬁc Languages
## Conclusion
## Bibliography

# <a name="emergence">12. Emergence</a>
## Getting Clean via Emergent Design 
## Simple Design Rule 1: Runs All the Tests
## Simple Design Rules 2–4: Refactoring 
## No Duplication
## Expressive
## Minimal Classes and Methods 
## Conclusion
## Bibliography

# <a name="concurrency">13. Concurrency</a>
## Why Concurrency? 
## Myths and Misconceptions
## Challenges 
## Concurrency Defense Principles
## Single Responsibility Principle 
## Corollary: Limit the Scope of Data 
## Corollary: Use Copies of Data 
## Corollary: Threads Should Be as Independent as Possible 
## Know Your Library 
## Thread-Safe Collections
## Know Your Execution Models 
## Producer-Consumer
## Readers-Writers
## Dining Philosophers 
## Beware Dependencies Between Synchronized Methods 
## Keep Synchronized Sections Small
## Writing Correct Shut-Down Code Is Hard
## Testing Threaded Code 
## Treat Spurious Failures as Candidate Threading Issues 
## Get Your Nonthreaded Code Working First
## Make Your Threaded Code Pluggable 
## Make Your Threaded Code Tunable
## Run with More Threads Than Processors
## Run on Different Platforms 
## Instrument Your Code to Try and Force Failures
## Hand-Coded 
## Automated 
## Conclusion
## Bibliography

# <a name="successive-refinement">14. Successive Refinement</a>
## Args Implementation 
## How Did I Do This? 
## Args: The Rough Draft 
## So I Stopped 
## On Incrementalism 
## String Arguments 
## Conclusion

# <a name="junit-internals">15. Junit Internals</a>
## The JUnit Framework
## Conclusion

# <a name="refactoring-serialdate">16. Refactoring SerialDate</a>
## First, Make It Work
## Then Make It Right
## Conclusion
## Bibliography


# <a name="smells-and-heuristics">17. Smells and Heuristics</a>
## Comments 
### C1: Inappropriate Information
### C2: Obsolete Comment
### C3: Redundant Comment 
### C4: Poorly Written Comment
### C5: Commented-Out Code 
**Just don't do it** If you want to do this; just slap yourself instead and ask what is wrong with me. Most people won't delete others commented out code since they assume there is a good reason for it. So it grows stale like a fine cheese(but bad cheese).



## Environment 
### E1: Build Requires More Than One Step
### E2: Tests Require More Than One Step 

## Functions
## F1: Too Many Arguments
## F2: Output Arguments 
## F3: Flag Arguments 
## F4: Dead Function 

## General 
### G1: Multiple Languages in One Source File
### G2: Obvious Behavior Is Unimplemented
### G3: Incorrect Behavior at the Boundaries 
### G4: Overridden Safeties 
### G5: Duplication
### G6: Code at Wrong Level of Abstraction
### G7: Base Classes Depending on Their Derivatives 
### G8: Too Much Information 
### G9: Dead Code
### G10: Vertical Separation 
### G11: Inconsistency 
### G12: Clutter
### G13: Artiﬁcial Coupling 
### G14: Feature Envy
### G15: Selector Arguments
### G16: Obscured Intent 
### G17: Misplaced Responsibility
### G18: Inappropriate Static
### G19: Use Explanatory Variables 
### G20: Function Names Should Say What They Do 
### G21: Understand the Algorithm 
### G22: Make Logical Dependencies Physical
### G23: Prefer Polymorphism to If/Else or Switch/Case 
### G24: Follow Standard Conventions
### G25: Replace Magic Numbers with Named Constants 
### G26: Be Precise
### G27: Structure over Convention
### G28: Encapsulate Conditionals 
### G29: Avoid Negative Conditionals 
### G30: Functions Should Do One Thing 
### G31: Hidden Temporal Couplings
### G32: Don’t Be Arbitrary 
### G33: Encapsulate Boundary Conditions
### G34: Functions Should Descend Only

## One Level of Abstraction 
### G35: Keep Conﬁgurable Data at High Levels
### G36: Avoid Transitive Navigation

## Java 
## J1: Avoid Long Import Lists by Using Wildcards
## J2: Don’t Inherit Constants 
## J3: Constants versus Enums 

## Names 
### N1: Choose Descriptive Names
### N2: Choose Names at the Appropriate Level of Abstraction
### N3: Use Standard Nomenclature Where Possible
### N4: Unambiguous Names
### N5: Use Long Names for Long Scopes
### N6: Avoid Encodings 
### N7: Names Should Describe Side-Effects. 

## Tests 
### T1: Insufﬁcient Tests 
### T2: Use a Coverage Tool!
### T3: Don’t Skip Trivial Tests 
### T4: An Ignored Test Is a Question about an Ambiguity 
### T5: Test Boundary Conditions
### T6: Exhaustively Test Near Bugs
### T7: Patterns of Failure Are Revealing 
### T8: Test Coverage Patterns Can Be Revealing 
### T9: Tests Should Be Fast

## Conclusion
