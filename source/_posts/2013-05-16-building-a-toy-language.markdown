---
layout: post
title: "Building a toy language"
date: 2013-05-16 11:28
comments: true
categories: Coding
---

Good morning guys! Today I've been trying to build a toy language. I found a little gem named [Treetop](https://github.com/nathansobo/treetop) which allows you to write a syntax file that can parse other files following those rules. It can also be used to parse code, for example. 

Using that gem I tried to code a little C-like language using Ruby, but later I found another [gem](https://github.com/aarongough/sexpistol) for parsing S-Expressions, which is what Lisp and Scheme use, and I decided to try it.

I quickly wrote what would be an example of my language, Kompressor (taken from Mercedes-Benz car engines):

```
(let my_name ("Pablo"))

(func hello() (
  (print "hello()" "\tHello" "\tHow are you?" "\tYou're cool!")

))

(hello ())

(print "cool_bro()")
(func cool_bro() (
  (if (3 == 3)
    (print "\tIf's in functions!")
  )
))

(cool_bro ())

(print "if statement")

(if (my_name <= 2)
  (print "\tHey! my_name is smaller than 2!")
)
```

Currently only can do the things in the example: `if` statements, function definitions, variable definitions and function calling. I also added the print method to output text to the screen.

But using Sexpistol to parse this was really messy, and I finally understood why Treetop generates nodes. When you're writing a language, you need to parse the code, and the optimal way is to use nodes for the different types. These nodes can identify a string, a variable definition, a function... And you later can do whatever you want with those nodes.

But although parsing seems hard, what really is hard is the evaluation time, when your language actually gets executed. You need your language perfectly parsed and ready to get evaluated, but you also need an environment to keep variable and function definitions. You also need to specify how these nodes interact with the data stored in the environment, for example:

```ruby

class FunctionCall < Base
  def eval(env)
    function = identifier.eval(env)
    puts "FunctionCall: #{arguments.inspect}"
    if arguments
      puts "FunctionCall: arguments present"
      function.call(env, arguments)
    else
      puts "FunctionCall: arguments not present"
      function.call(env)
    end
  end
end

```

This code would be a Treetop node specifying what to do when a function call is detected. As you can see, in this example it looks in the environment for a Ruby `proc` and calls it with the environment and the arguments (if present).

Although Ruby might not be the best choice to code a toy language, it's a valid option and it has a variety of [examples](https://github.com/jstotz/porkchop) [in](https://github.com/snusnu/trxl) [GitHub](https://github.com/snusnu/trxl) for example. It's also fun to see how a custom language that you completely made works!