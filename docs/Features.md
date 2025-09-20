<!-- For license of this file, see LICENSE.md in the base dir. -->

Features of Horse64 Root
===================

**WARNING, THIS PROJECT IS SUPER UNFINISHED, SOME OF THIS ISN'T
IMPLEMENTED YET.**

Keep in mind many statements in this document are
**subjective.** Nevertheless, Horse64 Root has the following features:

- Simpler than C++ or Rust, being a focused and streamlined
  lowlevel OOP language, [(see more about **streamlining**...)](
  #a-focused-design)

- Borrows its syntax and approachable look from [Horse64](
  https://horse64.org/),

- Great C inter-operability,

- Expert manual memory management as found in many
  systems programming languages,

- Ownership features for memory safety l/ike `defer`,
  `add_own()`/`del_own()`, and array length checks, [(see
  more about **safety**...)](#measured-safety)

- Avoids exceptions with instead a simpler `failable` handling,
  [(see more about **simple code flow**...)](#a-clear-code-flow)

- Amazing integration with the Horse64 ecosystem.

If you're a beginner, you may want to learn
[Horse64](https://horse64.org) instead.

For how to use Horse64 Root, [check out the
introduction](/docs/Introduction.md).

Read onward for more detailed feature explanations.

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
are easy to use, consistently used in practice, and clear:

- **Block-level `defer` makes safe cleanp easy.**
  This statement is 1. easy to understand,
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

- Using the `failable` semantics to easily check if a call
  succeeded via `failed()` avoids complex exceptions. Errors
  are propagated via a simple
  `return failed`.

- Using no async nor promises, the straightforward event facilities
  of the standard library try to avoid surprises.

- The object-oriented programming based on simple `struct`s is
  simple and very extensible via composition. No virtual overrides
  obscure code flow.


