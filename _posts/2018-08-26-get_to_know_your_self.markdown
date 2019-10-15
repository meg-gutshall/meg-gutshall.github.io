---
layout: post
title: "Get to Know Your Self (Refactored)"
date: 2018-08-26 13:23:53 -0400
featured-img: /img/post-images/eleham.jpg
# categories: [Flatiron School]
tags: [women in tech, WiT, tech, software development, Ruby, reserved words]
excerpt: <p>While Ruby is an incredibly user-friendly language, it’s not without its conundrums&mdash;one in particular being <code>self</code>. <code>self</code> is a Ruby reserved word that can be scoped to any class or instance of a class. This enables developers to contextually reference a particular instance or class&mdash;depending on what the needs are for their program&mdash;without using a specific variable name. It's not hard to see how this could quickly become confusing. Read on to walk through some simple examples and gain a better understanding of the concept of <code>self</code>.</p>
---

While Ruby is an incredibly user-friendly language, it’s not without its conundrums—one in particular: `self`. ``self`` is a Ruby reserved word, or a word specifically designed to have a special meaning in the Ruby language. The scope (or program visibility) of `self` is any class or instance of a class, which we can also refer to as an `object`. This means that `self` can enable developers to contextually reference a particular class or instance of a class—depending on what the needs are for their program—without using a specific variable name.

If the method is a message, who is the receiver? The object! Many times the object and `self` are one in the same, but sometimes they aren't. In the example below, I'll explain how `self` changes depending on the "message" that's being sent.

```ruby
class AfroPet
  attr_accessor :species
  @@all = []

  def initialize(species)
    @species = species
    @@all << self
  end

  def self.all
    @@all
  end
end

hipmo = AfroPet.new("Hippopotamouse")
eleham = AfroPet.new("Eleham")
ghound = AfroPet.new("Giraffet Hound")
```

The code above shows the `AfroPet` class which has a `species` attribute as well as an `@@all` class variable. Two methods have been defined as part of the `AfroPet` class: `#initialize` and `self.all`. In addition, three new species of `AfroPet` are created, including the pocket-sized Eleham!

![Elephant shrew in the Berlin Zoo](/img/post-images/eleham.jpg)

## `self` Referring to an Instance of a Class

We first see `self` being shoveled into the `@@all` class variable on Line 7, in the `#initialize` method. At this moment in the program, what is `self` referring to?

Remember that whenever we instantiate a new object (also referred to as creating a new instance of a class), we call `#new` on the class itself, then immediately call `#initialize` on the object _just_ created—like a one, two punch. By writing `@@all << self` into our `#initialize` method, we enable the new instance to be automatically saved into the `@@all` class variable at the time of creation instead of having to manually add it later, which saves us time and keeps our code DRY!

To refer back to my message analogy, in this example `#new` is the sender while the `#initialize` method is the message. Furthermore, since we find `self` being utilized _inside_ the `#initialize` method, it is considered part of what is called the method scope, confirming that `self` does indeed refer to the newly created object.

## `self` Referring to a Class

We next see `self` on Line 10 in the `self.all` class method. This is a class method designed to return the value of the `@@all` class variable, which is an array of instances of the `AfroPet` class. As you saw above, we created three new instances of the `AfroPet` class: `hipmo`, `eleham`, and `ghound`. So what happens when we call the `self.all` class method?

```ruby
AfroPet.all
#=> [#<AfroPet:0x000055b7db32c9c0 @species="Hippopotamouse">, #<AfroPet:0x000055b7db32c970 @species="Eleham">, #<AfroPet:0x000055b7db32c920 @species="Giraffet Hound">]
```

After typing `AfroPet.all` in our terminal, it returns an array containing our three previously-instantiated `AfroPet` objects, showing that the program recognizes that in this case, `self` is referring to the `AfroPet` class. We know this because the recipient of this particular "message" (or any class method as denoted with the `self.` prefix before the method name) is the class itself, which means that `self` is **_not_** scoped to any particular instance, but to the _class_ instead.

So how does `self` know when to change the object it’s referencing? Two ways:

1. The first being context as we have previous discussed above.
2. The second being a built-in rule for this reserved word: **_one and only one `self` will exist at any given time in the program._** There will never be a case in which `self` will refer to more than one object at a time, therefore leaving it up to context to determine what `self` actually means at any given point in the program.

<!-- vv Check this entire example. vv -->

I know, that’s a lot of information and your head is probably spinning by now, but let’s do one more example of `self`. I’ll walk you through it!

```ruby
class Creamery
  attr_accessor :creamery_name, :ice_cream_flavor, :creamery_flavors
  @@all = []

  def initialize(creamery_name, ice_cream_flavor)
    @creamery_name = creamery_name
    @ice_cream_flavor = ice_cream_flavor
    @creamery_flavors = []
    self.creamery_flavors << @ice_cream_flavor
    @@all << self
  end

  def new_flavor(ice_cream_flavor)
    @ice_cream_flavor = ice_cream_flavor
    self.creamery_flavors << @ice_cream_flavor
  end

  def self.all_creamery_flavors
    @@all.each {|creamery| creamery.creamery_flavors.each {|flavor| puts "#{creamery.creamery_name} " + flavor}}
  end
end

bnj = Creamery.new("Ben and Jerry's", "Chunky Monkey")
hersheys = Creamery.new("Hershey's", "Chocolate")
nelsons = Creamery.new("Nelson's", "Graham Slam")
```

After defining the `Creamery` class, we create three new creameries: `bnj`, `hersheys`, and `nelsons`.

In this example, the `#initialize` method creates a new creamery given the `creamery_name` and `ice_cream_flavor` attributes. Here we also declare an empty array called `@creamery_flavors` to store this creamery’s ice cream flavors. The `ice_cream_flavor` is added to the creamery’s `@creamery_flavors` instance variable and the creamery itself is added to the `@@all` class variable. _Remember: In the last example, we saw how `self` refers to the newly created object when used inside the `#initialize` method._

You can add a new flavor to a creamery by calling `#new_flavor` on that instance of creamery and declaring the new `ice_cream_flavor` as a String argument of the method. The new flavor is then added to the creamery’s `@creamery_flavors` array. Does the context in which `self` is used here look familiar? (Hint: See the `#initialize` method!)

```ruby
hersheys.new_flavor("Vanilla")
#=> ["Chocolate", "Vanilla"]
hersheys.new_flavor("Strawberry")
#=> ["Chocolate", "Vanilla", "Strawberry"]

bnj.new_flavor("Chubby Hubby")
#=> ["Chunky Monkey", "Chubby Hubby"]
bnj.new_flavor("Oat of this Swirled")
#=> ["Chunky Monkey", "Chubby Hubby", "Oat of this Swirled"]
```

Lastly, the `self.all_creamery_flavors` class method iterates over the creameries in the `@@all` class variable and displays all the ice cream flavors contained within the `Creamery` class. It works like this:

1. Iterate over the `@@all` class variable to access each creamery instance.
2. For each creamery, call `#creamery_flavors` to access their instance variable array of `ice_cream_flavor` attributes.
3. Chain the `#each` method on that to iterate again over this nested array, this time `puts`-ing out the flavors to the terminal.

The original `@@all` class variable will automatically `return` at the end of this method's execution.

```ruby
Creamery.all_creamery_flavors

"Ben and Jerry's Chunky Monkey"
"Ben and Jerry's Oat of this Swirled"
"Ben and Jerry's Chubby Hubby"
"Hershey's Chocolate"
"Hershey's Vanilla"
"Hershey's Strawberry"
"Nelson's Graham Slam"

#=> [#<Creamery:0x00005558bceb7e08 @creamery_name="Ben and Jerry's", @ice_cream_flavor="Oat of this Swirled", @creamery_flavors=["Chunky Monkey", "Chubby Hubby", "Oat of this Swirled"]>, #<Creamery:0x00005558bceb7d68 @creamery_name="Hershey's", @ice_cream_flavor="Strawberry", @creamery_flavors=["Chocolate", "Vanilla", "Strawberry"]>, #<Creamery:0x00005558bceb7cc8 @creamery_name="Nelson's", @ice_cream_flavor="Graham Slam", @creamery_flavors=["Graham Slam"]>]
```

You just learned `self`! If you feel you have a good grasp of the concept of `self`, celebrate with a scoop of your favorite ice cream! If not, check out the following helpful resources:

[Ruby `self`](https://learn.co/lessons/ruby-self-readme)<br>
[Self in Ruby: A Comprehensive Overview](https://airbrake.io/blog/ruby/self-ruby-overview)<br>
[Understanding `self` in Ruby](https://www.honeybadger.io/blog/ruby-self-cheat-sheet/)

...And then have a scoop of ice cream. :D

### Refactor Bonus Section

Over a year after I originally wrote this blog post, I had occasion to come back and review my old posts. _My God_ this one was **_not_** pretty! I tried to clean it up a bit and use better examples/explain them better. If you have any comments to add or see something that's glaringly wrong, please DM me on Twitter at @meg_gutshall or email me at meghan.gutshall@gmail.com.

In my second round of research, I found a remarkably interesting and high-level post on `self` in Ruby and wanted to share it as bonus content. **Warning:** This is confusing shit and I am still far away from feeling completely comfortable with it. If you're a beginner, I highly recommend you stick to the three links above and bookmark this one to revisit at a later date: [Metaprogramming in Ruby: It's All About the Self](https://yehudakatz.com/2009/11/15/metaprogramming-in-ruby-its-all-about-the-self/).

Also, I rewrote both of my code examples used above for this refactored blog post and wanted to show a method for the second example that could be of general use—it's just not necessarily related to `self`.

```ruby
class Creamery

  ...

  def all_flavors
    @creamery_flavors.each {|flavor| puts flavor}
  end

  def self.all_creamery_flavors
    @@all.each {|creamery| creamery.all_flavors}
  end
end
```

You may have noticed that we had to iterate twice in the blog post's `self.all_creamery_flavors` method. Here I created a `#all_flavors` instance method that iterates over the `@creamery_flavors` array, `puts`-ing each flavor just like the blog post example. The only difference is, this method is scoped to an individual creamery. Then, I refactored the `self.all_creamery_flavors` class method to call on the new `#all_flavors` instance method once it goes through its first iteration in accessing individual creamery instances.
