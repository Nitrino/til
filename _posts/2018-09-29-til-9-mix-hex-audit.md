---
layout: post
title:  "[#9] Check broken packages"
categories: elixir
---
Update dependencies in the project is time-consuming and dangerous work.
It is necessary to make sure that the library is not broken in the new release.
Fortunately, Hex has a command showing packages are no longer recommended to be used by their maintainers.

```sh
$ mix hex.audit
Dependency  Version  Retirement reason
distillery  1.3.3    (other) Custom commands are broken in this release
```
