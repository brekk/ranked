# ranked

Handle function arity as an n-tuple. Allows for convenient memoization of functions up to 9 arity!

[![Madlib Project Badge](https://img.shields.io/badge/madlib-purple?logo=github&logoSize=auto)](//github.com/madlib-lang/madlib) <!-- $MADLIB.projectBadge -->
[![ranked v0.0.1](https://img.shields.io/badge/v0.0.1-purple?label=version)](//github.com/brekk/ranked) <!-- $MADLIB.json.version -->

---

Use `ranked` if you have a function with arity (the number of arguments a function takes) between two and nine and want to have a unary function (a function which takes a single value) which takes an n-tuple instead.

```madlib
import Ranked from "ranked"

three = (a, b, c) => a ++ b ++ c
trois = Ranked.n3(three)
trois(#["hey", "nong", "man")) // heynongman
```

This makes it pretty convenient if you want to have a memoized function, as you can use the tuple of the arguments as the lookup:

```madlib
import IO from "IO"
import Math from "Math"

import Study from "Study"

import Ranked from "ranked"
import {memoize} from "ranked/Memo"


// watch and be amazed as this prints only twice!
powpow = pipe(
  IO.pTrace("runcheck"),
  R.n2(Math.pow),
)
memopow = M.memoize(powpow)

main = () => {
  memopow(2, 2) // prints: runcheck #[2, 2]
  memopow(2, 4) // prints: runcheck #[2, 4]
  memopow(2, 4) // prints: _nothing_
}
```

There's also a set of functions for converting from n-tuple functions to n-arity functions in `ranked/Unranked`. See the tests if you wanna see how to use them.
