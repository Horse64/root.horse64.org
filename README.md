
![Horse64 Root Title Logo](https://root.horse64.org/img/horse64rootlogo.png)


Horse64 Root Programming Language
=================================

**Horse64 Root** is a system language similar to C/C++,
reimagined with a focus on easy syntax, understandable
OOP, and some baked-in safety features. This is a sibling variant of
the main [Horse64 language](https://horse64.org) intended for lower
level components.

```Horse64 Root
import str from root.horse64.org

func main -> i32 {
    var s <- str.str("Hello from Horse64 Root!")
    if failed(str.str) {
        return -1
    }
    print(s)
    return 0
}
```

Its uses are:

- Simpler than C++, but still has competent
  object-oriented programming (OOP),

- Borrows its syntax and approachable look from [Horse64](
  https://horse64.org/),

- Has various memory safety features,

- Great C inter-operability,

- Suitable for systems level code and low level code.

- [See more...](https://codeberg.org/Horse64/root.horse64.org/src/branch/main/docs/Features.md)

**Currently unusable, stay tuned.**


### Useful starting points

- [Read introduction](https://codeberg.org/Horse64/root.horse64.org/src/branch/main/docs/Introduction.md),

- [Check project news](https://horse64.org/#news),

- [See the project license](https://codeberg.org/Horse64/root.horse64.org/src/branch/main/LICENSE.md),

- [Read the FAQ](https://codeberg.org/Horse64/root.horse64.org/src/branch/main/docs/FAQ.md).

This repository holds the code of the m64 stdlib, which is the m64 standard
library, and its main documentation. The code is officially hosted on
[Codeberg](https://codeberg.org/Horse64/root.horse64.org) with a GitHub
mirror. The code of the horsec compiler is part of the `core.horse64.org`
package instead.


Install & Build
---------------

The recommended way to install is [to get the prebuilt Horse64 SDK](
https://horse64.org/get) which includes [the horsec
compiler](https://codeberg.org/Horse64/root.horse64.org/src/branch/main/docs/Compilation.md) that handles Horse64 & Horse64 Root.


Where Is What?
--------------

If you want to contribute or report a bug, you'll find
the Horse64 ecosystem is made of a larger
bunch of projects. Due to that, **locating where each
component is** and where the code is, can occasionally
be challenging. Therefore, there's a
[handy resource list for finding projects and
code locations](
https://horse64.org/docs/Resources) to help you out.

