---
layout: post
title:      "Back To The Basics"
date:       2018-10-14 22:13:52 -0400
permalink:  back_to_the_basics
---

Transitioning back to Ruby can be a difficult task. The more you learn, the more you forget as well. That's why keeping at it and continuing to push forward is key. That being said, sometimes you have to go backwards to go forwards.

I've found myself going back to old lessons multiple times to remember how I did something before. I always remember how it works in general, but without more experience I still need reminders to get everything done. What I've probably reviewed the most times is the difference between the methods and the variables and how to write them. Understanding the environment makes everything make more sense, but knowing how to program it is another challenge. I do remember this basic setup for an Object-Oriented Class in Ruby though:

```
def Class
     attr_accessor :name
		 
		 @@all = []
		 
		 def initialize(name)
		      @name = name
					@@all << self
		end
		
		def self.all
		     @@all
		end
end
```

Of course there are other basic methods that can be in a lot of classes, but this was beaten into to me with all of the OO Ruby labs. Understanding the difference between local, instance and class was essential. Going back and reviewing some of the previous labs was necessary to remember how to program some of the newer labs. Programming knowledge will always build on itself. That's one of the biggest take aways for me. Forcing yourself forward without reminding yourself of how you got there can be detrimental. Going back to the basics and truly building the foundation to build on is essential for success. I've been going back to the basics, so I can become an advanced full stack web designer. 
