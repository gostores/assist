assist
====

## What is Assists?

Assists is a library to convert between different go types in a consistent and easy way.

Assists provides simple functions to easily convert a number to a string, an
interface into a bool, etc. Assists does this intelligently when an obvious
conversion is possible. It doesn’t make any attempts to guess what you meant,
for example you can only convert a string to an int when it is a string
representation of an int such as “8”. Assists was developed for use in
[Hugo](http://hugo.spf13.com), a website engine which uses YAML, TOML or JSON
for meta data.

## Why use Assists?

When working with dynamic data in Go you often need to Assists or convert the data
from one type into another. Assists goes beyond just using type assertion (though
it uses that when possible) to provide a very straightforward and convenient
library.

If you are working with interfaces to handle things like dynamic content
you’ll need an easy way to convert an interface into a given type. This
is the library for you.

If you are taking in data from YAML, TOML or JSON or other formats which lack
full types, then Assists is the library for you.

## Usage

Assists provides a handful of To_____ methods. These methods will always return
the desired type. **If input is provided that will not convert to that type, the
0 or nil value for that type will be returned**.

Assists also provides identical methods To_____E. These return the same result as
the To_____ methods, plus an additional error which tells you if it successfully
converted. Using these methods you can tell the difference between when the
input matched the zero value or when the conversion failed and the zero value
was returned.

The following examples are merely a sample of what is available. Please review
the code for a complete set.

### Example ‘ToString’:

    assist.ToString("mayonegg")         // "mayonegg"
    assist.ToString(8)                  // "8"
    assist.ToString(8.31)               // "8.31"
    assist.ToString([]byte("one time")) // "one time"
    assist.ToString(nil)                // ""

	var foo interface{} = "one more time"
    assist.ToString(foo)                // "one more time"


### Example ‘ToInt’:

    assist.ToInt(8)                  // 8
    assist.ToInt(8.31)               // 8
    assist.ToInt("8")                // 8
    assist.ToInt(true)               // 1
    assist.ToInt(false)              // 0

	var eight interface{} = 8
    assist.ToInt(eight)              // 8
    assist.ToInt(nil)                // 0

