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
