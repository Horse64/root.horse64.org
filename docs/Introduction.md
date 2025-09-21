<!-- For license of this file, see LICENSE.md in the base dir. -->

Introduction to Horse64 Root
============================

**Horse64 Root** is a system language similar to C/C++,
reimagined with a focus on easy syntax, understandable
OOP, and some baked-in safety features. This is a sibling variant
of the main [Horse64 language](https://horse64.org) intended for lower
level components.

- For a [📋 features list, **go here**](/docs/Features.md).

- There's also [an FAQ here](/docs/FAQ.md).

To build Horse64 Root programs and to manage dependencies, use [horp
](https://codeberg.org/Horse64/core.horse64.org/src/branch/main/docs/Resources.md#horp)
like you would for Horse64 programs. The compiler for Horse64 Root is [horsec
](https://codeberg.org/Horse64/core.horse64.org/src/branch/main/docs/Resources.md#horsec)
and part of the [📥 SDK](
https://codeberg.org/Horse64/core.horse64.org/src/branch/main/docs/Resources.md#sdk).


How to learn Horse64 Root
-------------------------

Since Horse64 Root is a sibling language to Horse64, this introduction
expects you to know how Horse64 works. Based on its sibling,
Horse64 Root was constructed with the following changes:


### Syntax, static types, and type annotations

The basic syntax of Horse64 Root is based on the
[Horse64 syntax](
https://codeberg.org/Horse64/core.horse64.org/src/branch/main/docs/Tutorials/Syntax.md), but altered for Horse64 Root `.m64` files.
Continue reading to learn the main changes.

Unlike Horse64 which is dynamically typed, Horse64 Root is
**statically typed** with mandatory type annotations:

```Horse64 Root
import str from root.horse64.org

func main -> bool {
    var s <- stir.str("Hello World!")
    if failed(str.str) {  # Note: this means string alloc failed.
        return no
    }
    defer s.destroy()

    print(s)
    return yes
}
```

For variables and function parameters, `<- ...type desc...` after
the declaration will annotate the parameter or variable type:

```Horse64 Root
var my_var <- i32 = 5
```
For function return values, `-> ...type desc...` right before the
code block will annotate the return type:

```
func my_func -> i32 {
    return 5
}
```

Function pointers work by inlining the function header inside `(...)`
parenthesis:

```Horse64 Root
func this_returns_a_func_ptr -> ((_<-i32) -> bool) {
    return std.as_ref(my_other_func)
}
```


### Memory management

Horse64 Root has no garbage collection, instead all used data
must be destroyed manually.

Usually, this is achieved by:

- for structs, by using a `defer x.destroy()`
  right after some [struct instance](#oop-with-structs)
  `x` was successfully initialized via `.init` or an
  init constructor short-hand:

  ```Horse64 Root
  var s <- std.str("Hello World!")  # Short-hand for s.init("Hello World")
  if failed(std.str) {
      return -1
  }
  defer s.destroy()
  # ...use `s` string here for whatever purpose...
  ```

- for allocated buffers or struct [`ref`s or `c_array`s](#ref-types),
  by using a `defer std.unalloc(x)` right after some
  `x = std.alloc(...)` to make sure the allocation is released
  again later:

  ```Horse64 Root
  var s <- byte c_array = std.alloc(256)
  defer std.unalloc(s)
  # ...use `s` array here for whatever purpose...
  ```

- for allocated arrays by using a `defer std.unalloc_array(x)`:

  ```Horse64 Root
  
  var s <- byte array = std.alloc_array(std.size_of(std.deref(s)), 256)
  defer std.unalloc_array(s)
  # ...use `s` array here for whatever purpose...
  ```

Of course you're allowed to keep values around for longer
as well rather than destroy them at the end of the block,
but then you have to ensure they get destroyed or unalloc'ed
somewhere later.

The `defer` keyword
runs a call delayed at the end of the current block,
which can e.g. be used for safe resource cleanup.


### OOP with structs

While Horse64's approach to user types is the `type` statement
which allows complex **object-oriented programming (OOP)**,
Horse64 Root's **default user type is the `struct`** statement.

The biggest difference is that struct instances are **passed
by value,** unless you use an explicit [`ref` variable](#ref-types) to
pass them around, unlike in Horse64 where user types
are passed by reference.

Also, structs don't allow any inheritance when using
object-oriented functions.

However, structs can be populated with func attributes
via `func name_of_struct.func_attr_name ...` just like in
Horse64, and extending structs via `extend struct` also
works just like in Horse64. Therefore, other than type
inheritance, all basic object-oriented pattern are available.


### `ref` types

Types marked with `ref` or with `c_array` are equivalent to
C's pointers.


### Function calls and overrides

Unlike Horse64, Horse64 Root does **not allow so-called "keyword
arguments"** that specify any default values. However,
Horse64 Root **has function overriding** for func attributes
on [structs](#oop-with-structs), which works as follows:

```Horse64 Root
struct MyTestStruct {
}

func MyTestStruct.hello failable {
    var s <- std.str("Hello there!")
    if failed(std.str) {
        return failed
    }
    defer s.destroy()

    print(s)
}

func MyTestStruct.hello_with_num(num <- f64) failable {
    var s <- std.str("Hello there! Here's a number: ")
    if failed(std.str) {
        return failed
    }
    defer s.destroy()

    s.add(num)
    if failed(s.add) {
        return failed
    }

    print(s)
}

func this_is_a_test failable {
    var my_struct <- MyTestStruct

    my_struct.hello(5)  # Will call .hello_with_num() override.
    if failed(my_struct.hello) {
        return failed
    }
}
```

Basically, if you call any func attribute (like `.hello`)
where there is a 2nd func attribute that starts with
the same name followed by an underline and a suffix (like
`.hello_with_num`), the 2nd func attribute is considered an
alternate override.

Any alternate override will be picked when the arguments
given, including their types, don't match the ones required
by the original func attribute but do match the ones of the
override.


