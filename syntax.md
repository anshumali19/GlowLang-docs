# GlowLang Syntax Guide

GlowLang is designed to be deeply intuitive and readable, blending the power of a modern systems-capable VM with the expressive elegance of natural language.

## Key Features
* **No Semicolons**: Statements end at the end of the line.
* **Natural Operators**: Read code like English using `when`, `is`, `is not`, `is in`, and `every`.
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
*(Note: If you are transitioning from other languages like Python, `print("text")` is also fully supported.)*

## 3. Conditionals (When)
Instead of traditional `if` statements, GlowLang uses the beautiful `when` keyword, paired with natural English operators. Conditionals are closed with the `end` keyword.

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
Loops in GlowLang use the `every` keyword. 

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
GlowLang has built-in functional utilities like `keep`, `apply`, `avg`, `root`, and `dist`. You can define inline functions using `lambda`.

```glow
let nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Filter list (keep evens)
let evens = keep(lambda(n): even(n), nums)
show "Evens:", evens

# Map list (double elements)
let doubled = apply(lambda(n): n * 2, evens)
show "Doubled:", doubled
```
