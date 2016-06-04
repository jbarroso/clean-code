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
## Bad Code
## The Total Cost of Owning a Mess
## The Grand Redesign in the Sky
## The Primal Conundrum
## The Art of Clean Code?
## What Is Clean Code?
## Schools of Thought
## We Are Authors
## The Boy Scout Rule
## Prequel and Principles
## Conclusion
## Bibliography

# <a name="meaningful-names">2. Meaningful Names</a>
## Introduction
## Use Intention-Revealing Names
## Avoid Disinformation 
## Make Meaningful Distinctions 
## Use Pronounceable Names
## Use Searchable Names 
## Avoid Encodings 
## Hungarian Notation 
## Member Preﬁxes
## Interfaces and Implementations 
## Avoid Mental Mapping 
## Class Names 
## Method Names
## Don’t Be Cute 
## Pick One Word per Concept
## Don’t Pun 
## Use Solution Domain Names 
## Use Problem Domain Names
## Add Meaningful Context 
## Don’t Add Gratuitous Context 
## Final Words 

# <a name="functions">3. Functions</a>
## Small!
## Blocks and Indenting
## Do One Thing
## Sections within Functions 
## One Level of Abstraction per Function 
## Reading Code from Top to Bottom: The Stepdown Rule
## Switch Statements 
## Use Descriptive Names
## Function Arguments
## Common Monadic Forms
## Flag Arguments 
## Dyadic Functions
## Triads
## Argument Objects
## Argument Lists 
## Verbs and Keywords
## Have No Side Effects 
## Output Arguments 
## Command Query Separation 
## Prefer Exceptions to Returning Error Codes 
## Extract Try/Catch Blocks 
## Error Handling Is One Thing
## The Error.java Dependency Magnet 
## Don’t Repeat Yourself 
## Structured Programming 
## How Do You Write Functions Like This? 
## Conclusion
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
