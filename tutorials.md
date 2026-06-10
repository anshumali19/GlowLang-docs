# GlowLang Tutorial: Building a Counter

Welcome to your first GlowLang tutorial! In this guide, we will walk through the basics of the language by building a simple counter that increments in a loop.

## Step 1: Outputting text
Let's start by printing a welcome message. In GlowLang, you don't need semicolons or brackets. Just use the `show` keyword!

```glow
show "Welcome to the Counter App!"
```

## Step 2: Creating a Blueprint
We want an object that holds a number and can increase it. We use a `blueprint` (GlowLang's version of a class) and define its methods as `action`s.

```glow
blueprint Counter:
    action init(start_value):
        self.val = start_value
    end
    
    action inc():
        self.val = self.val + 1
    end
end
```

## Step 3: Instantiating and Looping
Now we create our counter and use the `every` loop to increment it 5 times.

```glow
let my_counter = Counter(0)

every i in from 1 to 5:
    my_counter.inc()
    show "Counter is now at:", my_counter.val
end
```

## Step 4: Membership checking
Let's verify that the final value exists in a target list using the `when` and `is in` keywords.

```glow
let target_values = [3, 4, 5, 6]

when my_counter.val is in target_values:
    show "Target reached successfully!"
end
```

## Complete Code
Put it all together in a file called `app.glow`:

```glow
blueprint Counter:
    action init(start_value):
        self.val = start_value
    end
    
    action inc():
        self.val = self.val + 1
    end
end

show "Welcome to the Counter App!"
let my_counter = Counter(0)

every i in from 1 to 5:
    my_counter.inc()
    show "Counter is now at:", my_counter.val
end

let target_values = [3, 4, 5, 6]
when my_counter.val is in target_values:
    show "Target reached successfully!"
end
```

Run it using the GlowLang compiler!
