---
layout: post
title:  "(re)introduction to arrays in Ruby"
date:   2017-07-09 21:09:12 +0000
---


Now that I'm working through Ruby a second time, after the initial introduction at the beginning of the curriculum, I'm finding it to be **much** easier. I recently told someone that it feels almost as though I'm cheating this time around because I understand the concepts so much faster. 

As soon as I hit the array section, however, I slowed down.

The concept of iteration is still a bit confusing. I understand the idea of operating on every member of a collection but as I work to make my code more eloquent, it also becomes more abstract; that's where I tend to get lost. Lately I have been practicing writing code that may be a bit clunkier, getting it to pass the tests, and cleaning it up on a second pass. 

-----

The first lab where I encountered some difficulty after my relatively smooth re-introduction to Ruby was at the Square Arrays Lab. The prompt was straight-forward...

>You will build a method, square_array, that squares each element in an array of numbers and returns a new array of these squared numbers. Use an iterator and implement your own logic, don't use any built-in array methods other than .each (e.g. .collect, .inject).

...but the constraints around using built-in array methods stumped me. 

* First I thought I could just set every individual iteration equal to a new array that would populate as .each iterated over the original array:

```
def square_array(array)
 array.each do |integer|
  new_array = [integer ** 2]
  return new_array
 end
end
```

But this resulted in an array populated only with [1] instead of the expected [1, 4, 9].

* I thought perhaps the problem was that I was calling the new_array within the same body where I was iterating. So I separated it out:

```
def square_array(array)
 array.each do |integer|
  new_array = [integer ** 2]
 end
 return new_array
end
```

Predicatably, this resulted in an "undefined local variable or method" error.

* Then I decided to write the solution out in pseudo-code, while also hoping it would pass the specs:

```
def square_array(array)
 array.each do |integer|
  new_array = [integer ** 2, integer **2, integer **2]
  return new_array
 end
end
```

Well ... it didn't. Instead I got a new array of [1, 1, 1].

* Next I tried to work with the shovel method, which I thought may skirt the parameters of this lab a bit. But as long as I could get it past the specs it was fine with me:

```
new_array = []

def square_array(array)
 array.each do |integer|
  new_array << integer ** 2
 end
 return new_array
end
```

This time I got a second error around an undefined variable or method of new_array. 

* So I thought if I stuck the new_array into the method maybe I could get away with it:

```
def square_array(array)

 new_array = []

 array.each do |integer|
  new_array << integer ** 2
 end
 return new_array
end
```

AND IT WORKED. 

I'll be honest that I was frustrated to not be able to use .map or .collect but ultimaty I am pleased to have been forced to think creatively. 

-------

**Badges and Schedules Lab**

I found this lab to be a challenge as well. I think I had the hardest time with the first method that required me to iterate, #badge_batch_creator (also a bit of a tongue-twister - in hindsight I would use a different name here). 

I began by using .each but switched immediately to .collect since I kept getting an error about the return array. Each returns the original array, while map and collect both return a manipulated array. I also wanted to try out coding the method as succinctly as possible, with only one line of code in the body. 

```
def badge_maker(speaker)
 return "Hello, my name is #{speaker}."
end

speakers_lineup = ["Edsger", "Ada", "Charles", "Alan", "Grace", "Linus", "Matz"]

def batch_badge_creator(speakers_lineup)
 speakers_lineup.collect {|speaker| badge_maker(speaker)}
end
```

I had a little more trouble with #assign_rooms. I was trying to use .each_with_index to identify where in the array each element was located while also trying to return a new array. As soon as I figured out I could add .map to the end of .each_with_index it all fell into place.

```
def assign_rooms(speakers_lineup)
 speakers_lineup.each_with_index.map {|speaker, index| "Hello, #{speaker}! You'll be assigned to room #{index+1}!"}
end

def printer(speakers)
 batch_badge_creator(speakers).each do |badge|
  puts badge
 end
 assign_rooms(speakers).each do |assignment|
  puts assignment
 end
end
```
