---
layout: post
title: "Plato and OOP"
---

This post is a bit rough, but I haven't posted in a while, so I'm putting it up
here as a draft.

--------

Metaphysics is a hard topic to pin down. One formation is that metaphysics is
"the study of first principles." Another is that metaphysics seeks to answer
these two questions: "What things exist? What are those things like?" The
history of the word is complex, and the [SEP
article](http://plato.stanford.edu/entries/metaphysics/) on it is pretty great.

Plato is undoubtedly one of the most influential figures in philosophy, and his
metaphysics especially. His metaphysics also underpins object oriented
programming, thousands of years later. Let's dig into some Plato, and you'll
see what I mean.

## Theory of forms

Plato suggested a "theory of forms" to answer the questions posed by
metaphysics. There are two 'realms' that things can exist in: a material realm,
and a realm of forms. Plato's Theory of Forms is sometimes called "Platonic
idealism" for this reason. "Idealism" is a grouping of philosophies that assert
that reality is fundamentally of the mind, as opposed to as of the senses. And
so it is with Platonic Idealism: the realm of forms exists outside of our
perception, and is the more fundamental aspect of reality.

Let's talk more about forms. A form is an abstract kind of property, existing
separately from all other properties. These are also sometimes called
'essences,' because they are an essential property for whatever you're trying
to talk about.  As an example, consider 'computerness.' This is an abstract
idea of what it means to be a computer, separated from any particular computer
itself. These forms live in a realm of forms, completely separated from us.
However, if you can grok what it means to have 'computerness,' you can identify
things in our material world that have this property. We'd call those objects
'computers.' For example, a notebook is a computer, and a desktop is a
computer.  They're very different objects, but they both share this
'computerness' property, and are therefore computers. A computer isn't defined
by its screen, or its processing power, or its size or shape. It's defined by
'computerness.' A particular notebook, like the one that I'm writing this post
on, exists in the material world, but has a copy of many different kinds of
essences: it has computer-ness, it also has 'small-ness' and 'fragile-ness'
and a ton of other properties. Forms are one single property, but objects
can have a number of properties.

## OOP as realm of forms

So what does this have to do with object oriented programming? OOP is Plato's
Idealism, encoded in software. Let's look at the previous paragraph again, but
with Ruby code interspersed in between:


```ruby
# As an example, consider 'computerness.'
# This is an abstract idea of what it means to be a computer, separated from
# any particular computer itself.

module Computerness
  # computer-specific stuff goes here
end

# These forms live in a realm of forms, completely separated from us. 

Computerness.new # this fails, it cannot be instantiated

# For example, a notebook is a computer, and a desktop is a computer. 

class Computer
  include Computerness
end

notebook = Computer.new
desktop = Computer.new

notebook.is_a?(Computer) #=> true
desktop.is_a?(Computer) #=> true
```

As things change over time, they can gain properties, and therefore, become a
certain kind of thing:

```ruby
module Phoneness
end

class DumbPhone
  include Phoneness
end

class SmartPhone
  include Phoneness
  include Computerness
end

smartphone = SmartPhone.new
dumbphone = DumbPhone.new

dumbphone.is_a?(Phone) #=> true
smartphone.is_a?(Phone) #=> true

dumbphone.is_a?(Computer) #=> false
smartphone.is_a?(Computer) #=> true
```

My iPhone is just as much a computer as any other one I've owned, just in a
different form factor.

Personally, I am not a subscriber to Plato's theory of forms. I am also
becoming less and less of a fan of OOP, and I believe there's a direct
connection there.

So if not Platonic Idealism, what else? That's a topic for next time.
