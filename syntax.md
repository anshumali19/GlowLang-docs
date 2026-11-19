# GlowLang Syntax Guide

GlowLang reads close to plain English while running on a bytecode VM with a JIT compiler. This guide covers the essentials; the full [language reference](https://github.com/anshumali19/GlowLang-core/blob/main/docs/language_reference.md) has everything else.

## Key Features
* **No Semicolons**: Statements end at the end of the line.
* **Natural Operators**: Read code like English using `when`, `is`, `is not`, `is in`, and `every`.
* **Ends with `end`**: Blocks open with `:` and close with `end`.
* **Simple Output**: Use `show` to print anything without brackets. 

---

## 1. Variables and Data Types
Variables are declared using the `let` keyword. 

```glow
let x = 5
let my_list = [1, 2, 3, 4, 5]
let my_dict = {"name": "Glow", "version": 2}
```

## 2. Outputting Data
You can output data to the console using the `show` keyword. You do not need to wrap your arguments in brackets!

```glow
show "Processing numbers..."
show "x is:", x
```
*(`print` works as another name for `show`. Text can be joined with `+`, or written as an f-string: `show f"x is {x}"`.)*

## 3. Conditionals (When)
Conditionals use `when` (or `if`), with `eif` / `otherwise` (or `else`) for the other branches. `is` and `is not` mean `==` and `!=`. Conditionals are closed with the `end` keyword.

```glow
let x = 5
let z = 10

when x is 5:
    show "x is exactly 5!"
end

when x is not z:
    show "x and z are different"
end
```

### Membership Testing
You can cleanly check if an item exists within a list, string, or dictionary using `is in` and `is not in`.

```glow
let my_list = [1, 2, 3]

when 3 is in my_list:
    show "Found 3 in the list!"
end

when "z" is not in "abcde":
    show "z is missing from the string"
end
```

## 4. Loops (Every)
Loops in GlowLang use the `every` keyword (or `for each`); `from 1 to 5` includes both ends. 

```glow
show "Looping from 1 to 5:"
every i in from 1 to 5:
    show i
end
```

## 5. Object-Oriented Programming (Blueprints)
Instead of "classes", GlowLang uses `blueprint` to define structures and behavior. Methods are defined using the `action` keyword.

```glow
blueprint Counter:
    action init(val):
        self.val = val
    end
    
    action inc():
        self.val = self.val + 1
    end
end

let c = Counter(10)
show "c is:", type(c)

c.inc()
show "c.val after inc:", c.val
```

## 6. Functional Operations
Lists have `map`, `filter` and `reduce` methods, and the `natural` library adds English-style helpers:
`keep`, `apply`, `even`, `avg`, `root` and `dist`. Inline functions are written with `lambda`.

```glow
use "natural"

let nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
show "Squares:", nums.map(lambda(n): n * n)

# Filter list (keep evens)
let evens = keep(lambda(n): even(n), nums)
show "Evens:", evens

# Map list (double elements)
let doubled = apply(lambda(n): n * 2, evens)
show "Doubled:", doubled
```

## 7. Comments and Numbers
Comments start with `#` and run to the end of the line; `/* ... */` spans lines. `//` is floor
division, as in Python, and integers never overflow.

```glow
# a comment
show 7 // 2, -7 // 2, 7 % 3      # 3 -4 1
show 2 ** 100                     # 1267650600228229401496703205376
show 0xff, 0b1010, 1_000_000      # 255 10 1000000
show 6 & 3, 6 | 3, 1 << 10        # 2 7 1024
```

## 8. Functions: Defaults, Named Arguments, `...rest`, `**opts` and Spreading

```glow
func order(item, qty = 1, gift = false):
    return f"{qty} x {item}, gift: {gift}"
end
show order("tea", gift = true)    # 1 x tea, gift: true

func total(first, ...rest):
    return first + sum(rest)
end
let more = [2, 3, 4]
show total(1, ...more)            # 10

func tag(name, **attrs):          # **attrs collects the name = value arguments left over
    return name + " " + str(attrs)
end
show tag("p", id = "intro")       # p {"id": "intro"}
show tag("a", **{"href": "/"})    # a {"href": "/"}
```

## 9. Unpacking

```glow
let a, b = 1, 2
a, b = b, a
let first, ...others = [10, 20, 30]
show a, b, first, others          # 2 1 10 [20, 30]
```

## 10. Match and Enums

```glow
enum Level: LOW, MEDIUM, HIGH

func describe(value):
    match value:
        case 0:
            return "zero"
        case 1, 2, 3:
            return "small"
        case [head, ...tail]:
            return f"a list starting with {head}"
        otherwise:
            return "something else"
    end
end
show describe(2), describe([5, 6]), Level.HIGH    # small a list starting with 5 Level.HIGH
```

## 11. Sets and Comprehensions

```glow
let tags = {"web", "api", "web"}
show len(tags), "api" in tags                    # 2 true
show {1, 2, 3} & {2, 3, 4}                       # {2, 3}
show [n * n for each n in [1, 2, 3, 4] when n % 2 == 0]   # [4, 16]
show {w: len(w) for each w in ["glow", "lang"]}           # {"glow": 4, "lang": 4}
```

## 12. Working with `none`
`a ?? b` gives `b` only when `a` is `none`, and `a?.b` gives `none` instead of an error when `a`
is `none`.

```glow
let user = none
show user?.name ?? "guest"        # guest
let port = none
port ??= 8080
show port                         # 8080
```

## 13. Errors: `try`, `catch`, `finally`

```glow
func parse_age(text):
    try:
        let n = int(text)
        when n < 0:
            throw "age cannot be negative"
        end
        return n
    catch e:
        show "bad input:", e
        return none
    finally:
        show "checked", text
    end
end
show parse_age("41")
show parse_age("-3")
```

## 14. Generators
A function with `yield` in it hands over values one at a time, as they are asked for, so it can
even be endless. `next(g)` takes one value; `yield from` hands over every item of another
sequence.

```glow
func count_up(limit):
    let i = 0
    while i < limit:
        yield i
        i += 1
    end
end
show [n * n for each n in count_up(4)]   # [0, 1, 4, 9]
let g = count_up(2)
show next(g), next(g), next(g, "done")   # 0 1 done
```

## 15. With Blocks
`with` uses a resource for a block and lets go of it however the block ends, even on an error.
Objects take part with `enter()` / `exit(error)` methods, or just `close()`.

```glow
with sqlite.open(":memory:") as db:
    sqlite.exec(db, "CREATE TABLE notes (text TEXT)")
    sqlite.exec(db, "INSERT INTO notes VALUES ('hello')")
end                                       # db is closed here
```

## 16. Decorators
`@d` above a `func` makes the name hold `d(func)`, as in Python. `functools.cache` remembers
results; decorators work on methods too.

```glow
import "functools"

@cache
func fib(n):
    when n < 2:
        return n
    end
    return fib(n - 1) + fib(n - 2)
end
show fib(90)                              # 2880067194370816120, at once

func shout(f):
    return lambda(...args, **opts): str(f(...args, **opts)).upper() + "!"
end
@shout
func greet(name):
    return "hello " + name
end
show greet("asha")                        # HELLO ASHA!
```

The [language reference](https://github.com/anshumali19/GlowLang-core/blob/main/docs/language_reference.md)
covers every statement, operator and built-in function.
