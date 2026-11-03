# Topic 1: Overview
## 1.1 Programming Paradigms
-	_"A programming paradigm is a way to conceptualize and structure the implementation of a computer program"_
-	**A paradigm is not a feature.** Is more a **style**, how to model problems and organizing code. **It shapes your way** to write a solution for a problem.
-	Programming languages can be classified as supporting one or more paradigms, e.g.:
-	Imperative/procedural, object-oriented, functional or declarative/logic.
-	Some languages are built around a single paradigm, like **Prolog** for logic programming or **Haskell** for functional programming
-	Many others are multiparadigm and allow several styles side by side, e.g. Kotlin, Python, C#, which are combining imperative, object-oriented and functional features.

## 1.2 AI and Programming Languages
> _Are programming languages still relevant in the age of AI?_

**YES!**

Programming languages remain relevant in the age of AI because we still need a precise way to specify what a program should do. Natural language, even when structured in Markdown, has no formally defined semantics and is therefore ambiguous.
For example, _"student records must be sorted"_ leaves open the sort key, the direction, and the tie-breaking, whereas `ORDER BY grade DESC, lastname ASC` states the intended behaviour exactly.

## 1.3 Imperative programming
-	_"impera"_ = _"to command"_
-	A program is defined by a sequence of commands that **change** a program’s **state**.
-	Theoretical foundation: Turing machine.
-	Programs explicitly describe the control flow.
-	Concept:
•	Variables (memory locations)
•	Assignment: Change stored value over time
•	Control flow: goto or conditional jumps
-	Introduces **time** into the model by creating a temporal order between the evolving state.
-	Challenging to debug and to reason about. The state changes over time, side-effects have to be considered.
-	Models the working of early computers.
-	CPUs are imperative.

## 1.4 Challenging to reason about
What’s the intention of the following program?
```cpp
a = 1
b = 2
c = b
b = a
a = c
```
-	It swaps the variables, but it’s not easy to read.
-	"=" The equality character has another meaning than in maths, because you can change the variable.
-	In math the content of a variable stays, once it was assigned (immutable).

## 1.5 Assembly Language
> _"A programming language is low level when its programs require attention to the irrelevant."_<br>
> Alan Perils

-	**Low-Level** programming language
-	Strong correspondence between
    - Instructions in the language
    - Architecture’s machine code instructions
-	Typically, 1:1 statement per machine instruction
-	Use of mnemonics instead of machine codes
-	Pros:
    -	Full control over hardware and very fast
-	Cons:
    - Hard to write / read & change
    - not portable across different architectures (x86, x64, ARM, etc.)
    - no memory safety
Assembler: Translates assembly mnemonics into machine code (1:1, no optimization)

### 1.5.1 Example
ARM64 (AArch64) Assembly
```asm
.global _start
.align 2

_start:
mov x0, #0
mov x1, #10

loop:
add x0, x0, x1
sub x1, x1, #1
cmp x1, #0

exit:
mov x16, #1
svc #0x80

```

## 1.6 Procedural Programming
- Organize code in **procedures**, also called as **functions** or **subroutines**
    - Names
    - Parameter types
    - Return type
- **Control flow** within and between procedures is expressed through control structures
    - if / then / else
    - while / for
- Example languages:  Pascal, C, Fortran

## 1.6.1 Example
pascal
```pascal
program SumNumbers;

function Sum(n: integer): integer;
var
  i, total: integer;
begin
  total := 0;
  i := n;
  while i > 0 do
  begin
    total := total + i;
    i := i - 1;
  end;
  Sum := total;
end;

var
  res: integer;
begin
  res := Sum(10);
  writeln('Sum: ', res);
end.
```

## 1.7 Object-Oriented Programming
> _"I thought of objects being like biological cells and/or individual computers on a network, only able to communicate with messages."_
> Alan Key

- Organize **data** together with **code**
    - Objects with fields/attributes and methods
- Support for abstraction and modularization
    - Abstract data types, Information hiding
- Concepts:
    - Objects and messages (receiver)
    - Classes as a blueprint for objects and prototypes
    - Polymorphism, dynamic dispatch
    - Inheritancee for code reuse
- **Imperative in its core**
- Example languages: Simula, Smalltalk, Java, C#, C++

### 1.7.1 Example
Kotlin
```kotlin
class Dog(val name: String) {
    fun bark() {
        println("$name says: Woof!")
    }
}

class Person {
    fun pet(dog: Dog) {
        println("Petting ${dog.name}...")
        dog.bark()
    }
}

fun main() {
    val myDog = Dog("Rex")
    val person = Person()
    person.pet(myDog)
}
```

## 1.8 Declarative Programming
- **Express the logic of a computation without describing its control flow.**
- Describe **what** the program must accomplish in terms of the problem domain, **not how** to accomplish it.
- The language implementation figures out the best way to perform the computation.
- **Higher-level** languages, often based on theories of formal logic using deduction as computation.
- Sub paradigms:
    - Domain-specific languages
    - Logic programming
    - Functional Programming

## 1.9 Structured Query Language (SQL)
- Domain specific language to query databases
- A query defines what to find in a database, implementation decides how to retrieve the result.
- Theoretical foundation: Relational algebra

### 1.9.1 Example
```sql
SELECT DISTINCT l.name FROM Languages l
JOIN langConcepts lc ON lc.l_id = l.id JOIN Concepts c ON c.id = lc.c_id
WHERE c.`desc` LIKE '%lambda%' ORDER BY l.name;
```

## 1.10 Logic Programming
- Prolog is short for “programming in logic”
- Theoretical foundation: First-order logic (predicate logic)

### 1.10.1 A program consists of...
#### 1.10.1.1 Facts
`fact :- true`
```prolog
ancestor(pascal, java).
ancestor(java, kotlin).
ancestor(java, scala).
```
- In this case: `ancestor(pascal, java)` is a **compound term** (structure) with functor `ancestor` and arity 2, written `ancestor/2`.
- With the terminating period it is a **fact**: a clause with no body, unconditionally true.
- Reading: “pascal is an ancestor of java”. Argument order has no built-in meaning in Prolog; it is a convention you define, here `ancestor(Ancestor, Descendant)`.

#### 1.10.1.2 Rules
`head :- body` means `head <- body` (head is true if body is true)
```prolog
influenced(A, B) := ancestor(A, B).
% influenced(A, B) <- ancestor(A, B)

influenced(A, B) := ancestor(A, TMP), influenced(TMP, B).
% influenced(A, B) <- ancestor(A, Tmp) ∧ influenced(Tmp, B)
```
The rules define `influenced/2` as the **transitive closure** of `ancestor/2`: 
-	A influenced B if A is a direct ancestor of B (clause 1, base case)…
-	…or if A is an ancestor of some TMP that (transitively) influenced B. (clause 2, recursive case)

#### 1.10.1.3 Queries
To run a program, we ask questions about a database with a query
```prolog
?- influenced(pascal,X).
```
`X` is **unbound** and gets bound by unification. This is the difference from assignment: **Prolog does not “return” values**, it finds variable bindings that make the goal true.
The order of solutions follows the clause order in the program (having the base case first means direct influences come before indirect ones).






