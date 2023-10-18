# Kata: Stack programming language

A stack machine is virtual machine where operations happen against a stack. The
Java JVM is a stack machine, and so is the Python interpreter. It's also a
central concept in the Forth programming language, first designed in 1970. In
this Kata we're going to implement a simple stack-based programming language.

The central data structure is a stack: you can see a stack as an array where we
only `push` items to the end or `pop` them off again. The stack is a mutable
data structure, where `push` adds a single item to the end of the stack, and
`pop` pops the top item off the stack, reducing the stack by one.

We are going to implement a simple calculator stack machine. Here is an
interactive session where we do 1 + 2.

```
> 1
1
> 2
2
> +
3
```

What happens here is that first the stack is empty. Then 1 is pushed to the top
of the stack. After this 2 is pushed on top of it. The stack is now `[1, 2]`.
Then we issue the operation `+`, which pops the top two items of the stack and
replaces it with the result, 3. So in the end the stack is `[3]`. Each
interaction shows the top of the stack, so we can see what is happening.

## Do we implement the interactive example?

Note that this kata gives interactive examples throughout. That might easily
become an exercise in parsing, so it's not required to implement this. So we
will say you can interact with the stack machine programmatically using
function and method calls. There is a bonus item in the end to implement the
actual interactive command line. You can do this earlier if you want to,
though!

## Sums

Implement a stack machine where we can do simple sums as demonstrated above.
There doesn't need to be an interactive session yet; we can interact with it
using function or method calls.

We can push numbers onto a stack of numbers. We can also run the `+` operation
that takes the top two numbers from the stack and pushes back the sum.

How to deal with a stack underflow, when we try to take items from the stack
while the stack is empty? Just throw or return a programming language error in
this case.

## More arithmetic

Let's implement the other basic arithmetic operations as well: `-`, `*` and
`/`.

In the case of substraction given a stack `[a, b]` it should create a stack
with `a - b` on top. The same rule applies to division.

If we decide to divide by zero, the top of the stack should contain the special
value `<Error>`:

```
> 100
100
> 0
0
> /
<Error>
```

`<Error>` is not a number. How would you change the stack so it can take
non-numbers?

How would we calculate `(3 + 9) * (4 + 6)`? Write a test for that.

## Stack operations

- `swap` swaps the top two stack items, so `[c, a, b]` becomes `[c, b, a]`
- `dup` duplicates the top of the stack, so `[c, a]` becomes `[c, a, a]`
- `drop` drops the top of the stack, so `[c, a, b]` becomes`[c, a]`
- `over` takes a stack `[c, a, b]` and turns it into `[c, a, b, a]`

## Strings

Our language should support strings. If we enclose a value with double quotes
(`"`), we create a string literal:

```
> "foo"
"foo"
```

Make the `+` operator concatenate two strings if it encounters them on the
stack:

```
> "foo"
"foo"
> "bar"
"bar"
> +
"foobar"
```

What if `+` encounters a string and a number? It refuses to guess: we make that
an error value too:

```
> "foo"
"foo"
> 3
3
> +
<Error>
```

## Arrays

Our language could also place arrays on the stack:

```
> [1, 2, 3]
[1, 2, 3]
```

Make `+` concatenate arrays:

```
> [1, 2]
[1, 2]
> [3, 4]
[3, 4]
> +
[1, 2, 3, 4]
```

Combining arrays with non-arrays should be an error.

## New operations

It's useful to have definitions we can refer to by name, so we can easily
define new operations.

```
> square = dup *
defined: square
> 4
4
> square
16
```

The definitions are not stored in the stack: use a hash table (JS `Map` or
object) for them.

## Operations as stack values

Let's devise a way to place an operation on the stack (not its value). This
process is called "quoting". We also introduce a new operation `call` we can
use to call the top of the stack (if it's not a quoted operation, it's an
`<Error>`). We use the `'` character to quote:

```
> 3
3
> 'square
'square
> call
9
```

We can now implement `map`

```
> [1, 2, 3, 4]
[1, 2, 3, 4]
> 'square
'square
> map
[1, 4, 9, 16]
```

## Bonus: interactive command line

Implement an interactive command line as described throughout this kata.

How would you parse the various data structures?

How would you ensure it has tests?

## Bonus: more operations

We're getting pretty close to an actual programming language! The major area
missing concerning using booleans: we need various comparion operators (`> < == !=`) and boolean operators (`and or not`), as well as a way to do conditional
evaluation (`if`). Create them!
