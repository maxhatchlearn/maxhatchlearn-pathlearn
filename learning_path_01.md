Intro to Ruby
================================================================================

## Ruby Day 1

### Ruby Arrays

**Creating arrays**

Arrays store sequences of `objects`. There are a few ways to create an `array`:

        empty_array = Array.new
        another_empty_array = [] # this is the preferred way, and much easier!

        some_squares = [4, 9, 16]
        some_fruits = ["pear", "apple", "banana"]

![](pic.png)

### Ruby Strings

**Quotes**

Strings are how we represent text in Ruby. We need to protect the text from the Ruby interpreter so it doesn't think our text is actually code:

        > these are some words
        NameError: undefined local variable or method 'words' for main:Object
        from (irb):6
        from /Users/maxplomer/.rvm/rubies/ruby-1.9.3-p194/bin/irb:16:in '<main>'

********************************************************************************

## Ruby Day 2

### Learn Web Design, Coding & More at Treehouse

[![](http://img.youtube.com/vi/ZUAg51kA42M/0.jpg)](http://www.youtube.com/watch?v=ZUAg51kA42M)

### SF Scala: Martin Odersky, Scala -- the Simple Parts

[![](http://img.youtube.com/vi/ecekSCX3B4Q/0.jpg)](http://www.youtube.com/watch?v=ecekSCX3B4Q)

### Super Hard Ruby and JavaScript Exam

| problem type | coding                                         
|--------------|--------------------------------------------------------
| name         | Method Chains
| statement    | One may also chain method invocations by simply adding more periods and method names sequentially - each method in the chain is called on the result of the previous method. Go on and try it by invoking next twice on 1 to get 3.
| explanation  | The results you're looking at are the consequence of running a series of tests against your input to validate it. If you see results coloured red, this means one or more tests failed. Green means you're good to go.
| language     | Ruby
| start        | 1
| solution     | 1.next.next
| output       | 3
| description  | next called on 1 twice returns three


| problem type | coding                                         
|--------------|--------------------------------------------------------
| name         | Round Up!
| statement    | Use a JavaScript Math method to round up the number to next integer
| explanation  | Use Math.ceil()!!
| language     | JavaScript
| start        | 1.4
| solution     | Math.ceil(1.4)
| output       | 2
| description  | Math.ceil() method rounds number


| problem type | multiple choice                                         
|--------------|--------------------------------------------------------
| name         | Capitalize and Reverse
| statement    | How do you reverse and capitalize a string?
| explanation  | Ruby can do multiple methods called on top of one another.
| choice       | string.upcase.reverse
| correct      | true
| choice       | upcase(string).reverse
| correct      | false
| choice       | call upcase(string, output)
| correct      | false
| choice       | reverse(upcase(string))
| correct      | false


| problem type | checkbox                                         
|--------------|--------------------------------------------------------
| name         | First Array Element
| statement    | How do you get the first element of array? Check all of the code that is true.
| explanation  | Ruby has many ways to do the same thing.
| choice       | array.first
| correct      | true
| choice       | array.last
| correct      | false
| choice       | array[0]
| correct      | true
| choice       | array[1]
| correct      | false


| problem type | text prompt                                         
|--------------|--------------------------------------------------------
| name         | Favorite Part of Ruby
| statement    | What is your favorite part of ruby?
| explanation  | You can say whatever you want as long it is about Ruby programming language.

