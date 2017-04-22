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
* **Seiso**: Keep the workplace free of unusefull things (comments, etc).
* **Seiketsu**: Standarization. The group agrees about how to keep the workplace clean.
* **Shutsuke**: Discipline. Follow the practices.

You should name a variable using the same care with wich you name a first-born child.

They talk about that they found significant indicators that code with consistent indentation style had lower bug densitiy than code with bad indentation.

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
Nonsese: Programmers won't be needed because business people will generate programs from specifications.

The level of abstaction of our programing languages will increase but there will be code.

Well specified requirements can act as executable tests for our code.

## Bad Code

Bad code can bring a company down.

There are not excuses for bad code, no reasons: your boss does not give you time, you want to finish faster to get more backlog's stories finished...

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
* **No duplication, one thing, expressiviness, tiny abstractions**.
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
Insted of that use a name that specifies what is being measured and his unit:
```java
int elapsedTimeInDays;
```
Choosing names that reveal intent can make it much easier to understand and change code. What is the purpose of this code?

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
We can improve it only with reavealing naming:

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

Beware of using names that are very similiar *XYZFooBarClassForBlabla* and *XYZFooBarClassForBlablable*
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
If you can't pronouce it you can't discuss it without sounding like an idiot.
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
## Hungarian Notation 
## Member Preﬁxes
## Interfaces and Implementations 
Leave interfaces unadorened:
*ShapeFactory* and *ShapeFactoryImp* are better than *IShapeFactory* and *ShapeFactory*
## Avoid Mental Mapping 
*r* is the lower-cased version of the url with the host and scheme removed... WTF!

**Clarity is king**: professionals use their powers for good and write code that others can understand.
## Class Names 
A class name shoud not be a verb. Avoid words like Manager, Processor, Data, or Info.
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
Don't use slang!: whack() insted of kill()

**Say what you mean. Mean what you say.**
## Pick One Word per Concept
If you choose *get()* use it always (instead of fetch, retrieve, etc.)
## Don’t Pun 
Avoid using the same word for two puposes (*add()* method could mean different things in different classes...)

**Make your code as easy as possible to understand.**
## Use Solution Domain Names 
Use pattern names: Factory, Visitor, Decorator, etc.
## Use Problem Domain Names
And you could ask a domain expert if you have doubts.
## Add Meaningful Context 
Variables usually don't have a mean by themselves. You will need a context.

Names like: firstName, lastName, street, postalCode, etc. Are names from an address.

If you have problems with context you can add a prefix: addrFirstName, addrLastName, etc.

But It would be better if you put them into a class Adress => you will have a great context.

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
* Each function told a story.
* Each function led you to a next thing in a compelling order.

## Blocks and Indenting

The blocks within *if*, *else*, *while*, etc. statements should be one line long, probabily will be a function call.

This function call can have a nice an descriptive name

The indent level of a function should not be grater than one or two.

## Do One Thing

```
FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL. THEY SHOULD DO IT ONLY
```

A function do one thing though it contains calls to other functions. But those functions should be always one level bellow to the stated name of the funcion.

We create functions to decompose a larger concept (the name of the function) into a set of steps at the next level of abstraction.

## Sections within Functions 
A function that is divided into section will be probably doing more than one thing

## One Level of Abstraction per Function 
Don't mix level of abstraction in a function. This is always confusing an will bring you a broken window effect.

## Reading Code from Top to Bottom: The Stepdown Rule
Write code like if was a top-down set of TO-paragraphs.

## Switch Statements 
Switch statements always do N things.

Use them to create polymorphic objects. Abstract Factory pattern.

## Use Descriptive Names
You know that you are working with clean code when each routine turns out to be pretty much as you expected.

Use descriptive names. Don't be afraid to make a name long.

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
* Asking a question abouth that argument.*boolean fileExists("miFile")*
* Operating on that argument, tranforming and returning *InputStream fileOpen("miFile")*
* Events to alter the state of the system.

Try to avoid other forms.

## Flag Arguments 
Flag arguments (true|false) are ugly. Functions with that do one thing if it is true and another thing if is false.

Split the function in two:
*render(boolean isSuite) => renderForSuite() , renderForSingleTest()*

## Dyadic Functions
They are harder to understand than monadic functions.
*assertEquals(expected, actual)* ... where the expected should be? 

## Triads
The are harder to understand than dyadic functions.
*assertEquals(msg, expected, actual)* ... now the msg seems to be the expected value.

## Argument Objects
When a function needs to have more than two or three arguments some of these argument should be wrapped into a class of ther own.
*makeCircle(double x, double y, double radius) =>  makeCircle(Point center, double radius);*

## Argument Lists 
Function that takes argument lists can be monads, dyads or even tiads:
*void monad(String... args); void dyad(String name, String... args); void triad(String name, int count, String... args)*

## Verbs and Keywords
We can encode the name of the arguments into the funcion name:
*assertEquals => assertExpectedEqualsActual*

And we can do more meaning to the argument:
*write(name) => writeField(name)*

## Have No Side Effects 
Functions should not do things that you don't expect.
i.e: checkPassword(login, password) => inside initializes the user session.

## Output Arguments 
The should be avoided with OO.
*void appendFooter(StringBuffer report); => report.appendFooter();*

## Command Query Separation 
Functions should either do something or answer something, but not both.
*attributeExists and setAttribute* should be different functions. Avoid things like *setAndCheckIfExists*

## Prefer Exceptions to Returning Error Codes 
Error codes violate Comand Query Separation.

Exceptions can help to separate the happy path code from the error path and that helps to simplificate.

## Extract Try/Catch Blocks 
Try/catch's are ugly. It is better to extract try and catch methods.

## Error Handling Is One Thing
Methods with try/catch should only have this structure and nothing more.

## The Error.java Dependency Magnet 
Error codes are usually in classes like Error.java (whith constants). Avoid that, it is a dependency magnet (it is every where) and nobody wants to change it because you have to recompile/deploy everything.

Use Exceptions instead of Error coedes.

## Don’t Repeat Yourself 
Duplication may be the root of all eveil in software.

## Structured Programming 
Things like "there should only be one return statement" is unnecessary when you create small functions.

## How Do You Write Functions Like This? 
* Write ugly and long functions with a long list of arguments
* You need to have unit tests that cover all that functions.
* Then you can to massage and refine that code. You can break everything in clases and keep your test passing.
## Conclusion
Functions are the verbs and classes are the nouns of the language of our system.

You real goal is to tell the story of the System. You have to write functions that help yo to tell that story.
## SetupTeardownIncluder 
## Bibliography

# <a name="comments">4. Comments</a>
## Comments Do Not Make Up for Bad Code
## Explain Yourself in Code 
## Good Comments
## Legal Comments
## Informative Comments
## Explanation of Intent
## Clariﬁcation
## Warning of Consequences 
## TODO Comments
## Ampliﬁcation
## Javadocs in Public APIs
## Bad Comments 
## Mumbling 
## Redundant Comments 
## Misleading Comments
## Mandated Comments
## Journal Comments
## Noise Comments 
## Scary Noise 
## Don’t Use a Comment When You Can Use a
## Function or a Variable
## Position Markers
## Closing Brace Comments
## Attributions and Bylines
## Commented-Out Code
## HTML Comments 
## Nonlocal Information 
## Too Much Information 
## Inobvious Connection
## Function Headers
## Javadocs in Nonpublic Code 
## Example
## Bibliography

# <a name="formatting">5. Formatting</a>
## The Purpose of Formatting 
## Vertical Formatting 
## The Newspaper Metaphor 
## Vertical Openness Between Concepts 
## Vertical Density 
## Vertical Distance 
## Vertical Ordering 
## Horizontal Formatting
## Horizontal Openness and Density 
## Horizontal Alignment
## Indentation
## Dummy Scopes
## Team Rules
## Uncle Bob’s Formatting Rules

# <a name="objects-and-data-structures">6. Objects and Data Structures</a>
## Data Abstraction
## Data/Object Anti-Symmetry 
## The Law of Demeter
## Train Wrecks 
## Hybrids 
## Hiding Structure 
## Data Transfer Objects
## Active Record
## Conclusion
## Bibliography

# <a name="error-handling">7. Error Handling</a>
## Use Exceptions Rather Than Return Codes 
## Write Your Try-Catch-Finally Statement First 
## Use Unchecked Exceptions 
## Provide Context with Exceptions
## Deﬁne Exception Classes in Terms of a Caller’s Needs
## Deﬁne the Normal Flow 
## Don’t Return Null
## Don’t Pass Null 
## Conclusion
## Bibliography

# <a name="boundaries">8. Boundaries</a>
## Using Third-Party Code
## Exploring and Learning Boundaries
## Learning log4j 
## Learning Tests Are Better Than Free
## Using Code That Does Not Yet Exist
## Clean Boundaries 
## Bibliography

# <a name="unit-tests">9. Unit Tests</a>
## The Three Laws of TDD 
## Keeping Tests Clean 
## Tests Enable the -ilities
## Clean Tests 
## Domain-Speciﬁc Testing Language
## A Dual Standard 
## One Assert per Test 
## Single Concept per Test 
## F.I.R.S.T
## Conclusion
## Bibliography

# <a name="classes">10. Classes</a>
## Class Organization 
## Encapsulation 
## Classes Should Be Small!
## The Single Responsibility Principle
## Cohesion
## Maintaining Cohesion Results in Many Small Classes
## Organizing for Change 
## Isolating from Change
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
