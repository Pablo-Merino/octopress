---
layout: post
title: "Fiddling around with Ruby goodness"
date: 2013-05-20 08:35
comments: true
categories: Coding, Ruby
---

Yesterday I released [SimpleMongo](https://github.com/Pablo-Merino/SimpleMongo), an easy to set up ORM gem for MongoDB. In order to create an ORM I needed some model code that could allow me to write a model like:

```ruby

class MyTestClass
  include SimpleMongo::Model
  field :test

  validations do 
    validates_custom :test do |field|
      field == "something"      
    end
  end

  before_save do
    self.test = 'pablo'
  end
end

```

Even though it looks easy, this was a challenge to me. I needed to code a base model that allowed me to just include it in a real model and get everything working, just like an ActiveRecord model (or Mongoid model).

I learnt that way about `instance_eval` and `class_eval`. Also about the `self.included` method which is called when the module is included. In that method I could call `base.extend(ClassMethods)` where `ClassMethods` is just another module which has the class methods like `field` (so I can specify fields on the model), `before_save` callbacks and validations. These methods made defining a SimpleMongo model easier to read and simpler to write.

But how hard is to implement a similar behaviour? Once you figure it out it's not really hard! This is an example code:

```ruby
module Base
  def self.included(base)
    base.extend(ClassMethods)
  end

  module ClassMethods
    def say_hello(name)
      puts "hello #{name}!"
    end
  end
end

class MyClass
  include Base
  say_hello "Pablo"
end

MyClass.new
```

When you initialize that class, it calls `Base`'s `self.included` with the class instance as `base` argument. Then you extend the class with the methods in `ClassMethods`. That way you can build easy models with a nice DSL. 

After this I could implement the `field` method in my model to declare the fields I wanted to have. But this alone doesn't works! Wouldn't it be nice to be able to access the fields just within the model instance? For example:

```ruby

class MyTestClass
  include SimpleMongo::Model
  field :test

  validations do 
    validates_custom :test do |field|
      field == "something"      
    end
  end

  before_save do
    self.test = 'pablo'
  end
end

model = MyTestClass.new(:test => 'Yay!')

puts model.test # => 'Yay!'

```

You need to use the afore-mentioned `instance_eval` and `class_eval` on the `field` method, like:

```ruby
class_eval <<-EOS, __FILE__, __LINE__
        
  def #{name}
    keys[:#{name.to_s}]
  end

  def #{name}=(value)
    keys[:#{name.to_s}] = value
  end
EOS
      
instance_eval <<-EOS, __FILE__, __LINE__
        
  def #{name}
    keys[:#{name.to_s}]
  end

  def #{name}=(value)
    keys[:#{name.to_s}] = value
  end
EOS
```

That way you dynamically define getters and setters for the defined attributes (or fields). I think you don't need both `instance_eval` and `class_eval`, but I was having lots of problems with just one so I put both and worked just fine.

This is actually something I learned past Saturday, so there's sure a better way to implement it, as this one is buggy. I recommend you to check out [SimpleMongo](https://github.com/Pablo-Merino/SimpleMongo)'s source code and make pull requests with fixes and improvements if you feel like doing such task! :)
