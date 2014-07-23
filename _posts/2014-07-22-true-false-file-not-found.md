---
layout: post
title: "True, False, FileNotFound"
---

There's an old programming aphorism about the **tri-bool.** Your buddy heard from
a friend that the new intern was showing off some new code during code review,
and it looked like this:

    enum Bool { 
        True, 
        False, 
        FileNotFound,
    }

Ha ha, that silly intern. But at the same time, they're getting at something
much deeper: boolean logic is often too primitive to try and express what we're
trying to express. The mega-popular Boost library for C++ [contains a Tribool
implementation](http://www.boost.org/doc/libs/1_55_0/doc/html/tribool.html).
That intern isn't so silly now. But at the same time, boolean logic is at the
foundation of computing. What gives?

Well, here's the thing: a binary notion of truth is not usually a worthwhile
thing to even bother with, but binary truth colors everything in programming.
You can see this reflected at the simplest levels of computing. Boolean logic
is not that interesting or useful. At its most basic, you have a few simple
things:

1. Two values, `true` and `false`.
2. One binary operation: `conjunction` (`∧`)
3. One unary operation, `negation` (¬).

These operations are defined via **truth tables,** that look like this:

|   x   |   y   | x ∧ y |
|-------|-------|-------|
| false | false | false |
| true  | false | false |
| false | true  | false |
| true  | true  | true  |
 
and

|   x   |  ¬x   |
|-------|-------|
| false | true  |
| true  | false |

That's it. You may be wondering where `disjunction`(`∨`) went. Well, you can
pick either disjunction or conjunction as basic, as you can derive either of
them from the other:

     x ∧ y = ¬(¬x ∨ ¬y)
     x ∨ y = ¬(¬x ∧ ¬y)

Anyway, that's it. If you just memorize the above, you now know boolean logic.
And, in a certain sense, you now know _everything_ that computers can do.  To
put it in Rich Hickey terms, boolean logic is simple, but not easy. There's
just not a whole lot to it. In order to be useful, we combine these incredibly
primitive operations. For example, we can define `implication`(→) as

    x → y = ¬x ∨ y

Implication is the basis of the `if` statement: "if x, then y."

So, how does this relate to computing? We build **logic gates** out of some
kind of material. Originally, this was with diodes, and then transistors. We
map high levels of voltage to `true`, and low levels of voltage to `false`. We
can then build transistors that implement conjunction, disjunction, and
negation.

Here's what a conjunction gate looks like, as a diagram:

![AND gate](/img/and-gate.png)

But what's really interesting here is that you only need one kind of gate: the
NAND gate. This gate represents the operation `¬(x ∧ y)`. It's called a **NAND
gate** because computer scientists usually call conjunction, disjunction, and
negation by other names: AND, OR, and NOT. If you take a class on boolean logic
that's computer focused, your teacher will inevitably ask you to prove that you
can build the other primitive gates out of a NAND gate. Here, let's spoil your
homework. First, the symbol (and definition) for NAND:

     x ⊼ y = ¬(x ∧ y)

Building the other primitive operations:
 
     ¬x = (x ⊼ x)
     x ∧ y = (x ⊼ y) ⊼ (x ⊼ y)
     x ∨ y = (x ⊼ x) ⊼ (y ⊼ y)

That's it. You can expand out those definitions to actually prove it, I won't
bore you with that here, as it is _incredibly_ boring.

Speaking of boring, what's the point? Well, at first, I told you this: boolean
logic consists of two values and two operations. But I _also_ just told you
that you can derive those two operations from a single operation.  So which is
it? Well, you could make the argument that the `{true, false, ⊼}` version is
the most primitive, as it has three things, rather than four. You can _also_
make the argument that the `{true, false, ∧, ¬}` version is more primitive,
since, in a sense, ⊼ is constructed out of ∧ and ¬. But you can just define ⊼
through a truth table, not via ∧ and ¬. But does NAND even make sense without
not and and? Does it matter if it makes sense, given that it's just a name for
some function anyway?

So... what do we do? Is there an answer here? What is the Truth?

There isn't one. There are multiple truths, not one Truth. Which truth you
accept depends on which kind of problem you're interested in. Is 'minimalism'
to you conceptual beauty and simplicity? If so, then you probably care about
the four-definition. Is the 'minimalism' that you're interested in 'how few
kinds of transistors can I get away with manufacturing'? Then you probably care
about the three-definition. Or, you can simply not be interested in the
definition of a minimalistic definition of boolean logic at all, and so your
truth is FileNotFound.
