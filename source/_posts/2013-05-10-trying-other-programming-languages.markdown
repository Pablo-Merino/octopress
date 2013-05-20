---
layout: post
title: "Trying other programming languages"
date: 2013-05-10 07:25
comments: true
categories: Coding
---

If you know me, you'll know that I usually code in Ruby or Objective-C. I do love these languages and they're really powerful to me. 

With **Ruby** I can code any kind of webapp, or use it to build small scripts that will make my day-to-day easier. 

With **Objective-C** I can build both iOS and Mac apps, which is one of my hobbies.

But lately I've been trying other languages, such as Go, Java, Scala, Visual C#, C and C++:

### Go

**Go** is Google's programming language. It's really confortable to write code in Go if you've been a Ruby coder, mostly because it's pretty similar. It has the benefit of **being able to be compiled**, so it can run faster than a interpreted language (such as Ruby).

This would be an example Hello World:

``` go

package main

import "fmt"

func main() {
	fmt.Println("Hello, World")
}
```

Go also includes a **variety of libraries** ("packages") which make things such as network interactions and system calls to be easy as importing the library and using it.

### Java

Well, everyone knows Java, right? Well I sure do, and didn't liked it before trying it, and to be honest, that didn't changed after trying it. For an optimal Java development, you need to install Eclipse (although you can still code Java in your preferred editor and compile it from the command line), which is a **really RAM-hungry IDE**. Coding in Java is pretty easy, but sometimes it's stupid. I like the fact that you can make GUIs without a lot of effort.

Java is also used for Android development, something I wanted to try as well. Android development is a bit harder than just Java desktop apps, but once you get used to it's things, it's easy as well. In my work machine (which is a bit slow) **the Android VM took ages to boot**, and testing the app while you code it is pretty laggy as well. **Takes a few minutes to launch** it if you don't have enough RAM to keep a big heap space.

### Scala

I didn't really try Scala a lot, just wrote a few basic programs, so I can't really say a lot about it. It's based on Java, but **it's way more modernized than Java**. Unlike Java, **you don't need a specific IDE to code Scala**, just your favorite text editor and a console. Also unlike Java, you can write Scala scripts. This would be a Hello World script:

``` scala
#!/bin/sh
exec scala "$0" "$@"
!#
object HelloWorld {
  def main(args: Array[String]) {
    println("Hello, world! " + args.toList)
  }
}
HelloWorld.main(args)
```

I really have to discover Scala in a larger surface and see how it works on certain situations to be able to talk about it.

### Visual C#

When I started coding, I started with Visual Basic 6. Now we have Visual Studio 2012 where you can code in Visual Basic, Visual C#, C++, Windows 8 apps...

I don't really like Visual C# as well, but it sure is better than Visual Basic. In case you ever need to build a Windows app, y**ou should use Visual C# instead Visual Basic**, because it's going to be better on the long run. Visual C# looks like:

``` c#
using System;

class MainApp {

   public static void Main() {
      Console.WriteLine("Hello World using C#!");
   }
}
```

As you can see it has a Java-like syntax, but it's easier. The GUI building system is pretty easy as well, **offering a WYSIWYG editor which I actually like a lot**.

### C and C++

What can I say about C and C++? **C is one of the oldest languages available, yet it's really powerful. C++ is a version of C which is Object Oriented**. This makes the use of classes possible within C++, but still having all the C functionality. To be honest I'd rather code in C++, which would give me a lot of the Object Oriented advantages but still having C powerfulness.

A C++ Hello World would look like:

``` c++
#include <iostream>

int main(int argc, char *argv[])
{
  using namespace std;
  cout << "Hello World" << endl;
  return 0;
}

```

And now a C one:

``` c
#include <stdio.h>

int main(int argc, char *argv[])
{
 printf("Hello World\n");
 return 0;
}	
```

**It's also really easy to compile**, just needing `g++ -o hello_world hello_world.cpp` to build an executable. C's way would be almost the same, replacing `g++` with `gcc` (or `cc`) `gcc -o hello_world hello_world.c`.

---

I liked a lot to explore these languages, although I still feel I need to explore C-based languages and Scala a lot more. I'm not trying Java anymore, and I will be using Go in some future projects.