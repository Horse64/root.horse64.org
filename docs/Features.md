<!-- For license of this file, see LICENSE.md in the base dir. -->

Features of Horse64 Root
========================

**WARNING, THIS PROJECT IS SUPER UNFINISHED, SOME OF THIS ISN'T
IMPLEMENTED YET.**

Remember, this document is **subjective.** Here are Horse64 Root's features:

- Simpler than C++ or Rust, a streamlined lowlevel OOP language.
  [(Read about **streamlining**...)](#a-focused-design)

- Looks similarly approachable to [Horse64](https://horse64.org/).

- Designed for C inter-operability.

- Expert manual memory access as common for system languages.

- Features for better memory safety like `defer`, `own()`,
  `unown()`. [(Read about **safety**...)](#measured-safety)

- Avoids exceptions in favor of a simpler `failable` handling.
  [(Read about **simple code flow**...)](#a-clear-code-flow)

- Pairs up well with high-level [Horse64](https://horse64.org/).

If you're a beginner, e.g. if above list confuses you, try
[Horse64](https://horse64.org) first.

To get started with Horse64 Root, [check the intro](/docs/Introduction.md).

Read onward for more detailed technical feature explanations.


A focused design
----------------

Horse64 Root offers a modern, streamlined, and focused
design, with the following advantages:

- **Easy-to-read no-nonsense syntax with no historical baggage.**

  This makes jumping in easier for newcomers.

- **Core safety features are used mostly consistently.**

  Safety is not an afterthought.

- **Doesn't make safety features time-consuming to master.**

  It should be simpler to learn than e.g. Rust.


Measured safety
---------------

Horse64 Root brings lowlevel safety features that
are easy to use, used mostly consistently in practice, and clear:

- **Block-level `defer` makes safe cleanup easy.**
  This type of statement is 1. easy to understand,
  and 2. easy to use correctly compared to e.g. C's `goto error`
  or the comparatively complex code flow of a C++ exception.

  Meanwhile, it leaves the power of memory management in your hands.

- **Auto ref counting keeps track of memory ownership**, and it's
  integrated deeply into the standard library and used ubiquitously.

  This makes the language rather safe by default, rather than safety
  being an afterthought you need to go out of your way to implement.

- **No use of code flow obscuring exceptions.**
  There are no exceptions used like in C++ that would obscure the
  code flow. Instead, clean error passing is used.

- **High user-facing complexity was avoided,** to make it fun and
  approachable.

  For example, there is no complex garbage collector, no complex
  ownership semantics, no borrow checker, no complex
  asynchronicity, no complex error types, and so on.


A clear code flow
-----------------

Horse64 Root tries to make the code flow and side effects obvious:

- **The `failable` attribute provides painless error passing.**
  It allows easily checking if a call
  succeeded via `failed()` without disrupting normal code flow and
  without complex exceptions.

- **Straight forward code flow without async nor promises.** The
  straightforward event facilities of the standard library try to
  avoid surprises. If you want high-level async, [use
  Horse64](https://horse64.org/) instead.

- **Simple object-oriented programming based on simple `struct`s** is
  simple and very extensible via composition. No virtual overrides
  obscure code flow.

  
Comparison with other languages and use cases
---------------------------------------------

⚠️⚠️⚠️ **Horse64 Root is currently very unfinished. The following
information is more of a roadmap, not the current state.** ⚠️⚠️⚠️

Here's a comparison to
[Python](https://python.org),
[JavaScript (JS)](https://www.javascript.com/),
[Go](https://go.dev/), and
[C++](https://cplusplus.com/). *Disclaimer: this list is
subjective, **no guarantee of accuracy**.*

[Please report inaccuracies.](/docs/Resources.md#report-bugs).


### Syntax, Core, and Code Flow Features

|H64 Root|Python|JS|Go|C++|Lua|Syntax, Core, and Code Flow             |
|--------|------|--|--|---|---|----------------------------------------|
| |✔|✔| | |✔|**Dynamic types** as a beginner-friendly default.         |
|✔|✔| |✔|✔|✔|**Strongly typed** to avoid silent harmful conversions.   |
|〰|✔| |✔| |✔|**Minimal, clean syntax** without line terminators.       |
|✔|✔|❓|✔|✔| |**Type annotations** can be used for extra verbosity.     |
|✔| | |✔|✔| |**Advanced type checker** verifies types ahed of time.    |
| |✔|✔| | |✔|**Minimizes concurrency crashes** in buggy code.          |
|✔| |✔|〰|✔|✔|**Line breaks optional** for versatile code layout.       |
| | |〰|✔| | |**Concurrency** of all I/O and network default APIs.      |
| |✔|✔|✔|✔| |**Garbage-Collector** to make avoiding leaks easier.      |
|〰|✔|✔|✔| |✔|**Object-oriented class types** as built-in feature.     |
|✔| |〰|✔| |〰|**Extend types without inheriting** as built-in feature.  |
| |✔| | |✔| |**Native multiple bases inheritance** for mixins.         |
| | | |✔| | |**Auto-parallel threaded execution** of every async call. |
| | | | |❓|✔|**Tail-call optimization** enabled by default.            |
|✔| | | | |✔|**1-based indexing** that is more beginner-friendly.      |

### Multimedia and Desktop App Features

(⚠️ Horse64 Root isn't great here, try Horse64 instead!)

|H64 Root|Python|JS|Go|C++|Lua|Libraries and Desktop App Features      |
|--------|------|--|--|---|---|----------------------------------------|
| |✔|〰|✔|〰| |**Big standard library** without extra setup.             |
|〰| |✔| | | |**UI and graphics integrated** for easy graphical apps.   |
| |✔|✔|✔| | |**High-level networking by default** for servers etc.     |
|〰|✔|✔|✔|❓| |**Unicode with full grapheme support** by default.        |

### Deployment Features

|H64 Root|Python|JS|Go|C++|Lua|Deployment Features                     |
|--------|------|--|--|---|---|----------------------------------------|
|✔| | |✔|✔| |**Portable program binaries** as default output.          |
|✔| | |✔|✔| |**Self-contained, no install** needed for end users.      |
|✔|✔| |✔| | |**Official packaging tools** for easy project handling.   |
| |✔|✔|❓| |✔|**Compiler trivially usable at runtime**, if needed.      |
|✔| | |❓|❓| |**Easily bake in all binary resources** like images.      |
|✔| | |❓| | |**Virtual archive mounting** for all standard I/O.        |
| |❓|❓|✔|✔| |**Can make C API libraries** easily for C/C++ program use.|

### Scripting Features

(⚠️ Horse64 Root can't do this at all!)

|H64 Root|Python|JS|Go|C++|Lua|Scripting Features                      |
|--------|------|--|--|---|---|----------------------------------------|
| |✔|✔|❓| |✔|**Compiler trivially usable at runtime**, if needed.      |
| |✔|✔| | |✔|**Instant script use** for fast script helper launch.     |
| |〰|✔| | |✔|**Easy runtime `eval()`** for trivial script injection.   |
| | |✔| | | |**Runs in web browser** by default, for simple web use.   |
| |✔|✔| | |✔|**Embedded easily** for integrated, subordinate scripts.  |
| |✔|✔| | |✔|**Easy runtime module loading** for trivial mutability.   |
| |✔|✔| | |✔|**Dynamic global scope** at runtime, extreme mutability.  |
| |✔|✔|❓| |✔|**REPL shipped by default** for dynamic experiments.      |

### Large Project Features

|H64 Root|Python|JS|Go|C++|Lua|Tooling and Large Project Features      |
|--------|------|--|--|---|---|----------------------------------------|
|✔| | |✔|✔| |**Precompiled** always, for better large project checks.  |
|✔| | |✔|✔| |**Static name resolution** to catch most typos early.     |
|✔| | |✔|✔| |**Non-trivial optimizations and warnings** by default.    |
|✔| | |✔|✔| |**Forced type declarations** for deepest compile checks.  |
| |✔|✔| | |✔|**Focused clean syntax** to write larger projects fast.   |

### Organizational Structure Comparison

|H64 Root|Python|JS|Go|C++|Lua|Organizational Structure Comparison     |
|--------|------|--|--|---|---|----------------------------------------|
|✔|✔|〰|✔| |✔|**One central default runtime** for combined efforts.    |
|✔|〰| |✔|✔| |**Default compiler self-hosted**, for easier changes.    |

### Runtime Performance and Lowlevel Features

|H64 Root|Python|JS|Go|C++|Lua|Runtime Perf. and Lowlevel Features     |
|--------|------|--|--|---|---|----------------------------------------|
| |✔|✔| | |✔|**Bytecode interpreter** for high portability.            |
|✔| | |✔|✔| |**Attribute lookups largely AOT**, to avoid bottlenecks.  |
|✔| |❓|✔|✔| |**Compiler made for AOT optimizations.**                  |
|✔|〰| |✔|✔| |**Largely lock-free memory sharing** for fast threading.  |
|✔| |✔|✔|✔| |**Always uses JIT** for speed, or 100% AOT compiled.      |
|✔| | |✔|✔| |**Outputs machine code** always, for extreme speed.       |
|✔| | | |✔| |**Fully manual allocations** easily available.            |

*(AOT refers to Ahead-of-Time, handled at compile time rather than
runtime.)*

For an easier to use high-level language, [see Horse64's list](
https://horse64.org/docs/Features#comparison-with-other-languages-and-use-cases).


Why not Rust?
-------------

Horse64 Root aims to be easier to learn, easier to write, better
to adapt and maintain, and with lower hardware demands for developers.

The perceived rigidness and high barrier for entry of Rust, as well as
the high memory needs making compilation on older hardare difficult,
is what led to the decision to work on an alterantive.

Whether that alternative succeeds, is for you to judge.

