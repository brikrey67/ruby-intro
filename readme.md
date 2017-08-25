# Ruby Basics

## Learning Objectives

* Compare/contrast Ruby and Javascript as programming languages
* Run Ruby code by REPL and file
* Identify specific differences between Ruby and Javascript in the following areas...
  - Syntax
  - Variables
  - Fundamental Data Types
  - Data Collections
  - Conditionals
  - Methods (Functions)
  - Data Immutability
* Examine Ruby symbols and data immutability
* List three useful methods for arrays and hashes

## Framing (10 minutes / 0:10)

### What is Ruby?

Ruby is a **server-side** programming language. We will be writing Ruby code that _serves_ webpages.

What is a server?
* It gathers information from the database, filters it using logic and from that generates something to send back to the user. That could be HTML or, in the case of an API, JSON.
* That means you cannot look at or mess with a site's server-side code as you did with Javascript via the browser console
* We won't be including Ruby files in our HTML documents. You'll learn more about back-end development and how to connect everything together next week.

### The Ruby Philosophy

#### M.I.N.A.S.W.A.N.

* Yukihiro Matsumoto ("Matz") created Ruby in the mid-90s to increase developer happiness
* "Matz Is Nice And So We Are Nice"
* Mentality not only applies to how you should treat your fellow developers, but also the philosophy behind Ruby itself

> "Programmers often feel joy when they can concentrate on the creative side of programming, so Ruby is designed to make programmers happy." — Yukihiro "Matz" Matsumoto  

![He really is quite nice.](matz-n-park.png)

#### A **Natural** Language

While it isn't exactly simple, a lot of its features are going to feel intuitive

> "Ruby is simple in appearance, but is very complex inside, just like our human body." — Yukihiro "Matz" Matsumoto  

## Tools We'll Be Using (5 minutes / 0:15)

We will be running Ruby code via the Terminal in two different ways. But first, let's make sure you're all set up...

### Setting Up Ruby

Check to make sure you have Ruby installed by running this in the Terminal: `$ ruby -v`
* Should get back something like: `ruby 2.4.0p0 (2016-12-24 revision 57164) [x86_64-darwin16]`
* If nothing shows up, run the following: `$ rvm install 2.4`

### Running Ruby

#### By File

```bash
$ touch app.rb        # Create a Ruby file
$ ruby app.rb   # Run that ruby file
```

#### By REPL

Just like Javascript and the browser console, we can use tools like Pry and IRB to run Ruby in a REPL.
  1. Install: `$ gem install pry`
  2. Run REPL: `$ pry`
  3. Quit from REPL: `exit`
  4. Alternative: `$ irb`

> A `gem` is a tool or application written in Ruby. We install them by entering `$ gem install gem_name` in the Terminal. Explore [rubygems.org](https://rubygems.org/) if you're interested in learning more.

## Ruby vs. Javascript: Differences in Syntax (10 minutes / 0:25)

### You Do: Turn And Talk (2 minutes)

Think back to the [Try Ruby homework you just completed](https://github.com/ga-wdi-exercises/try-ruby).

With a partner, write down some differences in syntax, "nice" or otherwise, you noticed between Ruby and Javascript.

### Variables

We no longer need to precede new variables with `var`. Just use the name of the variable!
* Variables are instantiated as they are used
* Written in `snake_case`. That means all lower case with words separated by underscores.
* Variable names should still be semantic

Variables are still assigned using a single equals sign ( `=` )

```rb
my_favorite_animal = "flying squirrel"
# => "flying squirrel"
```

Although we don't use `var`, there is still syntax to designate whether a variable is local or global.
* `$` makes it global (e.g., `$my_number`)
* Undesignated implies `local` (e.g., `my_number`)
* All-caps makes it a constant. That is, Ruby will give you warnings if you try to change the value (e.g., `PI = 3.14`).

### No Semicolons

While your code will work if you close a line with `;`, common practice is not to use them.

### Parentheses Optional

Since we're currently in a Javascript state of mind, it might feel natural to keep using them. That's okay! Ruby, however, does not require we use them when defining functions, conditional statements, etc.

```rb
number = 3
# => 3

if( number == 3 ) # with parens
  puts( "It's a 3!" )  
end  
# It's a 3!
# => nil

if number == 3 # without parens
  puts "It's a 3!"  
end  
# It's a 3!
# => nil
```

### `puts` and `gets`

`puts` is the equivalent of Javascript's `console.log()`

```rb
puts "Hello, Ruby!"
# Hello, Ruby!
# => nil
```

Ruby also allows us to easily accept inputs from the command line using `gets`

```rb
user_input = gets
# => "My input\n" (Note that this line was typed by the user in the terminal)

user_input
# => "My input\n"
```

Some notes about `gets`...
* Usually `gets` is followed by `.chomp`, which removes the new line generated by the user hitting return
* If you need to convert your value to a number, add `.to_i` to the end of the method

Let's test `gets` by using it in a Ruby file...

```rb
# Run this code in app.rb

# Asks for and stores a command line input into the variable as a string.
puts "How old are you?: "
user_input = gets.chomp.to_i
if user_input > 10
  puts "You are older than ten"
end
```

```bash
# In the terminal from in the same directory as app.rb

$ ruby app.rb
# => How old are you?:
20
# => You are older than ten

$ ruby app.rb
# => How old are you?:
8
```

## You Do: Data Types (15 minutes / 0:40)

Spend 15 minutes reading through everything up until the **[Data Types Exercises](#you-do-data-types-exercises)** section below this one.

> **Why do we have to read all this ourselves?**
>
> While we could re-teach you what numbers, strings, conditionals, etc. are like in Ruby, you know enough about programming languages from your experience with Javascript to pick up on this information yourself pretty quickly.
>
> Because of this, the peculiarities of Ruby will be apparent. These are the things you need to be aware of in the next few classes.

### Everything Is An Object!

Everything in Ruby is an **object**.
* By "object" we mean that everything has its own set of properties and methods
* Not a new concept. Some data types in Javascript had their own properties and methods (e.g., `string.length`)
* You will learn more about this when you dive into Ruby OOP next week

### Numbers

Ruby uses same arithmetic operators as Javascript
* `+`, `-`, `*`, `/`, `%`
* Same order of operations too: P.E.M.D.A.S.  

```rb
1 + 2 # Addition
# => 3

6 - 5 # Subtraction
# => 1

5 * 2 # Multiplication
# => 10

30 / 5 # Division
# => 6

31 / 5 # Note: integer division
# => 6

30 % 5 # Modulo (remainder)
# => 0

31 % 5
# => 1

3 ** 2 # Exponentiation
# => 9
```

> Notice the use of `**` to perform exponential operations in Ruby. We don't have this shortcut [in Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/pow).

### Strings

Words, just like in Javascript.
* Surrounded by single or double-quotes
* Ruby uses similar escape characters
  - [Here is a list of them](http://www.java2s.com/Code/Ruby/String/EscapeCharacterslist.htm)
  - Must instantiate string with double-quotes for escape characters to work

```rb
name = "John"
# => "John"

full_name = "John\nDoe"
# => "John\nDoe"

puts full_name
# John
# Doe
# => nil
```

Not only can you concatenate strings, now you can multiply them too! Remember we couldn't do that in Javascript?

```rb
# Concatenation
"Hello " + "there!"
# => "Hello there!"

# Multiplication
"Hello there! " * 3
# => "Hello there! Hello there! Hello there! "
```

#### String Interpolation

Sometimes you will want to print out a string that incorporates a variable. For example...

```rb
my_name = "Nayana"
# => "Nayana"

puts "Hi my name is: " + my_name
# Hi my name is: Nayana
# => nil
```

This works fine. Things aren't so simple when that variable is of a different data type. Like a number...

```rb
class_number = 984
# => 984

puts "I am teaching WDI " + class_number
# TypeError: no implicit conversion of Fixnum into String from (pry):26:in `+'
```

In cases like the above, you either need to convert the variable to a string using `.to_s` or use something called "interpolation."
* Surround the non-string variable with a hashtag and curly brackets: `#{variable}`. If you choose this option, you must use double quotes otherwise the interpolation will not work.
* No Javascript equivalent [(until ES6 came along)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)

```rb
class_number = 984
# => 984

puts "I am teaching WDI #{class_number}"
# I am teaching WDI 984
# => nil
```

### Booleans

Still `true` and `false`.
* We'll be using them in conditionals and comparisons just like in Javascript

Comparison operators in Ruby are nearly identical to Javascript. However, the check for equality is always for both value and data type.
* `<`, `>`, `<=`, `>=`, `==`, `!=`

> Don't worry about `===` in Ruby for now. It [does not](http://mauricio.github.io/2011/05/30/ruby-basics-equality-operators-ruby.html) have the same application as in Javascript.  

Logical operators are also similar.
* `!`, `&&`, `||`

"Truthiness" and "falsiness" are a lot less complicated in Ruby.
* The only falsey values in Ruby are `nil` and `false`

### Nil

Ruby's "nothing".
* The equivalent of Javascript's `null`
* You will usually see it when something does not have a return value (e.g., a `puts` statement)
* Like in Javascript, `nil` is falsey

Need to check if something is `nil`? Use `.nil?`  

> **NOTE:** Any method that ends with a `?` means it will return a boolean value.  

```rb
something = "A thing"
# => "A thing"

something.nil?
# => false

something = nil
# => nil

something.nil?
# => true
```

### The Bang Symbol (`!`)

All of the Ruby data types we have discussed so far are mutable.
* We can not only change what variables are pointing to in memory, but we can directly modify those values stored in memory as well.

Methods with an `!` attached to the end of them usually mean that they will modify the value in memory they are being called on.
* Things can get tricky when you have multiple variables pointing at the same value. For example...

```rb
a = "cheeseburger"
# => "cheeseburger"

b = a
# => "cheeseburger"

b.upcase!
# => "CHEESEBURGER"

a
# => "CHEESEBURGER"
```
### Symbols

Symbols are immutable values. That means they contain the same value through the entirety of a program and cannot be changed.
* Kind of like a string that never changes
* Syntax: `variable_name = :symbol_name`
* No Javascript equivalent [(until ES6 came along!)](http://www.2ality.com/2014/12/es6-symbols.html))

```rb
favorite_animal = :dog
# => :dog

favorite_animal.upcase!
# NoMethodError: undefined method `upcase!' for :dog:Symbol
# Did you mean?  upcase
```

When/why would you use symbols?
* Most common use is as keys in hashes, the Ruby equivalent of objects (more on that later)
* Make sure values that need to be constant stay constant
* Enhance performance, use less memory

### Conditionals

Pretty similar to Javascript, with some differences.
* No parentheses or curly brackets required
* Begin blocks using `if`, `elsif` **(no second "e"!)** and `else`
* We close the whole loop using `end`
  - This will be used throughout Ruby when dealing with code blocks (e.g., method/function)

Here's an example where we check for height at a roller coaster...

```rb
# In app.rb

puts "Welcome to the Iron Rattler! How tall are you (in feet)?"
height = gets.chomp.to_i

if height < 4
  puts "Sorry, you'll fly out of your seat if we let you on."
elsif height < 7
  puts "All aboard!"
else
  puts "If you value your head, you should not get on this ride."
end
```

## You Do: Data Types Exercises (15 minutes / 0:55)

Complete the first set of exercises (Exercise I: Data Types) in [this repo](https://git.generalassemb.ly/ga-wdi-exercises/ruby-basics-exercises).

If you finish this section early, feel free to try out one of the [Additional Exercises](https://git.generalassemb.ly/ga-wdi-lessons/ruby-intro#additional-practice) located at the bottom of the lesson plan.

### Break (10 minutes / 1:15)

## You Do: Data Collections (10 minutes / 1:25)

Read everything up until the [Data Collections Exercises](https://git.generalassemb.ly/ga-wdi-lessons/ruby-intro#you-do-data-collections-exercises-25-minutes--150) section below this one.

### Arrays

An ordered collection of related values. Same syntax as Javascript arrays.
* Square brackets
* Values separated by commas
* Zero-indexed

```rb
numbers = [1, 2, 3]
# => [1, 2, 3]

animals = ["dog", "cat", "horse"]
# => ["dog", "cat", "horse"]

animals[0]
# => "dog"

animals[1] = "elephant"
# => "elephant"

animals
# => ["dog", "elephant", "horse"]
```

Another super cool Ruby feature is that you can perform arithmetic operations on arrays!

```rb
numbers = [1, 2, 3]
# => [1, 2, 3]

more_numbers = [4, 5, 6]
# => [4, 5, 6]

lots_of_numbers = numbers + more_numbers
# => [1, 2, 3, 4, 5, 6]

lots_of_numbers - [4, 5, 6]
# => [1, 2, 3]

numbers * 3
# => [1, 2, 3, 1, 2, 3, 1, 2, 3]
```

#### Array Methods

Ruby is very nice. It provides us with an extensive library of array methods we can use to traverse and manipulate arrays.
* [The Ruby documentation for `Array` is a great resource for learning more about these methods](http://ruby-doc.org/core-.0/Array.html)
* Can't go over them all, but chances are if you could do it in Javascript then you can do it in Ruby.

**IMPORTANT:** You DO NOT need to memorize these. The following is just a sample of array methods available to you. You'll come to be more familiar with these as you need them and look them up in documentation.  

> **tl;dr:** The more you Google them, the better you'll remember them.  

##### Push/Pop

These Javascript methods also exist in Ruby and are used the same way.

```rb
numbers = [1, 2, 3, 4, 5]
# => [1, 2, 3, 4, 5]

numbers.push(6)
# => [1, 2, 3, 4, 5, 6]

numbers.push(7, 8, 9)
# => [1, 2, 3, 4, 5, 6, 7, 8, 9]

numbers.pop
# => 9

numbers
# => [1, 2, 3, 4, 5, 6, 7, 8]
```

##### Sort

Organizes array values from lowest to highest. Numbers and strings.

```rb
numbers = [3, 1, 5, 2, 4]
# => [3, 1, 5, 2, 4]

numbers.sort
# => [1, 2, 3, 4, 5]
```

##### Delete

* Removes an argument from an array
* If there are multiple instances of that argument, it will delete them all
* Look up: `.delete_at()`, `.slice()`

```rb
numbers = [3, 1, 2, 2, 4]
# => [3, 1, 2, 2, 4]

numbers.delete(2)
# => 2

numbers
# => [3, 1, 4]
```

### Hashes

A Ruby hash is an unordered, dictionary-like collection organized by key-value pairs. A hash is very similar to a Javascript object.

```rb
wdi_class = {
  teacher: "John",  
  students: ["Yacko", "Wacko", "Dot"],  
  classroom: 2,  
  in_session: true,  
  schedule: {  
    morning: "Ruby Basics",
    afternoon: "Enumerables"
  }
}  
# => {:teacher=>"John", :students=>["Yacko", "Wacko", "Dot"], :classroom=>2, :in_session=>true, :schedule=>{:morning=>"Ruby Basics", :afternoon=>"Enumerables"}}
```

Accessing hash values...  

```rb
wdi_class[:teacher]
# => "John"
```

Modifying hash values...

```rb
wdi_class[:teacher] = "Jack"
# => "Jack"
```

You can also use strings as hash keys...

```rb
wdi_class = {
  "teacher" => "John",  
  "students" => ["Yacko", "Wacko", "Dot"],  
  "classroom" => 2,  
  "in_session" => true,  
  "schedule" => {  
    "morning" => "Ruby Basics",
    "afternoon" => "Enumerables"
  }
}  
```

Then can access in this way...

```rb
wdi_class["teacher"] = "John"
# => "John"
```

And modify...

```rb
wdi_class["teacher"] = "Jack"
# => "Jack"
```

> Note the use of `=>` (or "hash rockets") instead of `:` when using strings as keys.  

#### Hash Methods

Like arrays, Ruby also provides us with a library of hash methods.  
* [Again, the Ruby documentation is a great resource](http://ruby-doc.org/core-2.4.0/Hash.html)

> As mentioned with arrays, do not worry about memorizing these methods. Just know how to look them up should the need arise.  

##### Keys

Returns an array with all the keys in a hash.

```rb
wdi_class.keys
# => [:teacher, :students, :classroom, :in_session, :schedule]
```

##### Merge

Combines two hashes. If both of your hashes have the same key, the one in the hash you set as the argument in the parameters will take precedence.

```rb
classroom = {
 room: 1  
}  
# => {:room=>1}

locations = {
 location_one: "DC",  
 location_two: "NY",  
 location_three: "Boston"  
}  
# => {:location_one=>"DC", :location_two=>"NY", :location_three=>"Boston"}

silly_hash = classroom.merge(locations)
# => {:room=>1, :location_one=>"DC", :location_two=>"NY", :location_three=>"Boston"}

classroom
# => {:room=>1}

locations
# => {:location_one=>"DC", :location_two=>"NY", :location_three=>"Boston"}

silly_hash
# => {:room=>1, :location_one=>"DC", :location_two=>"NY", :location_three=>"Boston"}
```

### Ranges

Use ranges to quickly generate arrays of data types.
* Parentheses
* Min and max value, separated by two periods
* Generate array using `.to_a` method

```rb
(1..5).to_a
# => [1, 2, 3, 4, 5]

("a".."z").to_a
# => ["a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z"]
```

## You Do: Data Collections Exercises (25 minutes / 1:50)

> 15 minutes exercise. 10 minutes review. 

Complete the second set of exercises (Exercise II: Data Collections) in [this repo](https://git.generalassemb.ly/ga-wdi-exercises/ruby-basics-exercises).

If you finish this section early, feel free to try out one of the [Additional Exercises](https://git.generalassemb.ly/ga-wdi-lessons/ruby-intro#additional-practice) located at the bottom of the lesson plan.

## Break (5 minutes / 1:55)

## Methods (10 minutes / 2:05)

As stated before, everything in Ruby is an object so there is no distinction in this language between functions and methods. Under the hood, even seemingly stand-alone functions are in fact associated with an object. The convention, however, is to call these methods.

Components
* `def` - the Ruby equivalent of `function`
* `double` - the method name in the below example
* `number` - the argument name in the below example
* `end` - closes the method

```rb
def double( number )
   doubled_number = number * 2
   return doubled_number
end  

double( 3 )
# => 6

double 3
# => 6
```

You may have noticed that we use the same `return` notation as Javascript. This is called an **explicit return**, because we identify what exactly we want returned from the function.  

Ruby also lets us make **implicit returns**.
* This means that we do not need to use the `return` keyword. Ruby will automatically return the value of the last line of code in the method.
* We encourage you to use **explicit returns** so we know exactly what your method is returning

```rb
def double( number )
  doubled_number = number * 2  
  doubled_number  
end  
# => :double

double( 3 )
# => 6

double 3
# => 6
```

Ruby methods can also establish default argument values.
* In the below example, if we do not provide our `double` method with an argument, it will default to 5

```rb
def double( number=5 )
  doubled_number = number * 2  
  puts "Your doubled number is #{doubled_number}"  
  doubled_number  
end  
# => :double

double
# Your doubled number is 10
# => 10
```

## Exercise: Temperature Converter (25 minutes / 2:30)

> 15 minutes exercise. 10 minutes review.

[Temperature Converter (Ruby)](https://git.generalassemb.ly/ga-wdi-exercises/temperature_converter_ruby)

-----------

## Bonus: Variables and Mutability (10 minutes)

Let's talk about variables and memory allocation in Ruby.

![XKCD pointers comic](https://camo.githubusercontent.com/e015a8e243f53ffecd9b18fc5c8d770dde1948cc/687474703a2f2f626c6f672e70726f7465637465647374617469632e636f6d2f77702d636f6e74656e742f75706c6f6164732f323030372f30352f706f696e746572732e706e67)

Why is that so funny? Because variables are pointers to values in memory.

![Variables in memory diagram](https://camo.githubusercontent.com/62b04af497f124fc9b11ec3802d73497f5c9e305/687474703a2f2f64326177357865326a6c647175652e636c6f756466726f6e742e6e65742f626f6f6b732f727562792f696d616765732f7661726961626c65735f706f696e74657273312e6a7067)

<a href="https://imgflip.com/gif/t9736"><img src="https://i.imgflip.com/t9736.gif" title="made at imgflip.com"/></a>

### Retrieving Memory Location

We can use the `.object_id` method to demonstrate that two variables are pointing to the same object.
* Returns an integer identifier for the object that is automatically generated by Ruby
* Lets use `.object_id` to demonstrate that the first diagram in this lesson is true

```rb
a = "hi there"
# => "hi there"

b = a
# => "hi there"

a.object_id
# => 70096095324100

b.object_id
# => 70096095324100

a = "not here"
# => "not here"

a.object_id
# => 70096094155620

b.object_id
# => 70096095324100
```

### The Bang Symbol (`!`)

All of the Ruby data types we have discussed so far are mutable.
* We can not only change what variables are pointing to in memory, but we can directly modify those values stored in memory as well

Methods with an `!` attached to the end of them usually mean that they will modify the value in memory they are being called on.
* Things can get tricky when you have multiple variables pointing at the same value. For example...

```rb
a = "cheeseburger"
# => "cheeseburger"

b = a
# => "cheeseburger"

b.upcase!
# => "CHEESEBURGER"

a
# => "CHEESEBURGER"
```

### You Do: Ruby Variables Exercise (15 minutes)

> 10 minutes exercise. 5 minutes review.

Test out what you just learned with this [Ruby variables exercise](https://git.generalassemb.ly/ga-wdi-exercises/ruby_vars_exercise)

--------

## Questions

* What are Ruby's 5 main data types?
* Describe the difference between what is truthy/falsey in Ruby vs JavaScript?
* What's the difference between explicit and implicit return?
* How would you add a key / value pair to an existing hash?
* How many values can a method return? Which methods don't return anything?

## Resources
* [Learn X in Y minutes: Ruby](https://learnxinyminutes.com/docs/ruby/)
* [Chris Pine's Learn to Program](https://pine.fm/LearnToProgram/chap_00.html)
* [Ruby Monk](https://rubymonk.com/)
* [Why's Poignant Guide to Ruby](http://poignant.guide/book/chapter-2.html)
* [Ruby Koans](http://rubykoans.com/)
* Screencasts
  - [WDI8, Ruby Preview](https://youtu.be/Be4YGLovGM4)

## Additional Practice
* [Word Ladder](https://git.generalassemb.ly/ga-wdi-exercises/word_ladder)
* [Who Won The Election?](https://git.generalassemb.ly/ga-wdi-exercises/who_won_the_election)
* [Search For Obi-Wan](https://git.generalassemb.ly/ga-wdi-exercises/search_for_obi_wan)
* [Pig-Latin](https://git.generalassemb.ly/ga-wdi-exercises/pig_latin)
* [Letter Counter](https://git.generalassemb.ly/ga-wdi-exercises/letter_counter)
