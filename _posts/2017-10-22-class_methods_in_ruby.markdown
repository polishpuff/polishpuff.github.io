---
layout: post
title:      "Class Methods in Ruby"
date:       2017-10-22 09:14:21 -0400
permalink:  class_methods_in_ruby
---

A topic I've recently encountered that gave me trouble was class variables and methods in OO Ruby. I tried to learn object-oriented programming in the past (a year or so ago, on my own) and did not understand it AT ALL. This time around the concepts made a lot more sense immediately, which was pleasantly surprising. I love that I can use variables across different methods - it makes programming so much easier. The pieces giving me the most trouble are (1) remembering all the rules for instance vs. class methods/variables and (2) putting the concepts of OO programming together with array and hash operators. 

The most recent lab, 'Class Variables and Methods Lab', gave me a lot to think about. The prompt gives instructions to create a Song class along with instance variables & methods (name, artist, genre) and class variables & methods (count, genres, artists, genre count, artist count) that all interacted with one another and with the Song class (self).

The two last class methods proved the most difficult for me to work with. @@genre_count and @@artist_count are meant to be hashes that count the types of genres and artists out of each respective array and return that total, with the genre/artist name as the key and the count as the value. I confess I had to Google how to iterate through the array and increment count, but this turned out to be a great lesson in different ways of arriving at the same answer.

I want to provide the code leading up to these two class methods, for context:

```
class Song

  attr_accessor :name, :artist, :genre

  def initialize(name, artist, genre)
    @name = name
    @artist = artist
    @genre = genre
    @@count += 1
    @@genres << genre
    @@artists << artist
  end

  @@count = 0

  def self.count
    @@count
  end

  @@genres = []

  def self.genres
    @@genres = @@genres.uniq
  end

  @@artists = []

  def self.artists
    @@artists = @@artists.uniq
  end

```

I knew I had to start with the bones of the method:

```
def self.genre_count
end
```

First I tried working with the ternary operator in a way that made the most sense; in previous labs I realized that hashes have trouble recognizing values for keys that don't yet exist so I tried to actively avoid having this problem by checking for a key and pushing in corresponding values:

```
def self.genre_count
 @@genre_count = {}

 f = genre.count
 @@genre_count.has_key? ? @@genre_count[genre] << f : @@genre_count[genre] = genre
end
```

This threw an ArgumentError, which continues to mystify me. I'm not sure where I'm missing arguements, but I think there are some additional issues with this code. For example, I don't refer to the array @@genres anywhere in the block, which I'm certain I have to do in order to get it working. However, I do appreciate having the chance to practice working with the ternary operator (some code ? if true do this thing : if false do this other thing). I like how elegant and brief it is. 

Then I tried incrementing the count using += 1 but had issues there as well:

```
def self.genre_count
 @@genre_count = {}
 
 @@genres.inject(@@genre_count) {|total, e| total[e] += 1; total}
end
```

and 

```
def self.genre_count
 @@genre_count = {}
 
 @@genres.each {|genre| @@genre_count[genre] += 1}
end
```

But both of those gave me: "NoMethodError: undefined method `+' for nil:NilClass". I did some research and realized that this kind of error is a problem when @@genre_count[genre] is nil instead of 0. There is a lot of [hepful advice](https://stackoverflow.com/questions/37715446/undefined-method-for-nilnilclass-ruby) about how to set to 0 to avoid this error but none of the advice I could find dealt explicitly with hashes, so it wasn't that relevant.

Some additional research pointed to using #group_by on the array to return distinct groups of genres. I haven't worked with #group_by before and I'm so pleased I discovered it. [This blog](http://gregpark.io/blog/ruby-group-by/) gives a rundown of useful ways to use #group_by. In this case I paired it with (:&itself), which is a method that groups itself into an array; more on that [here](http://www.rubydoc.info/github/rubyworks/facets/Object%3Aitself). This also led me down a path of trying to learn more about the &: syntax, which I'm still having some trouble with. [This](http://www.brianstorti.com/understanding-ruby-idiom-map-with-symbol/) piece is particularly helpful although I don't understand closures or #to_proc as of yet.

In any case, I ended up with this code:

```
def self.genre_count
 @@genre_count = {}
 
 @@genres.group_by(&:itself).each {|k, v| @@genre_count[k] = v.count}
end
```

This returned just the array of group_by (sidenote: it's kind of cool to see what's going on in group_by by accident here):

```
{"rap"=>["rap", "rap"], "pop"=>["pop"]}
```

I jumped into pry to see what was happening, since this answer was so close to what I was expecting. @@genre_count was returning without any problems in pry, which made me realize what I was missing in the code was to return my hash (this is a frequent issue for me, so I need to watch it moving forward). The code I ended with was:

```
def self.genre_count
 @@genre_count = {}

  @@genres.group_by(&:itself).each {|k,v| @@genre_count[k] = v.count}

 return @@genre_count
end
```

Woo! 






