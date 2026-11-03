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




