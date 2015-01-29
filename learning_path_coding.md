Ruby And JavaScript Coding Exercises
================================================================================

## Coding Exercises Module

### Simple Ruby and JavaScript excercises

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
| name         | Growing arrays
| statement    | Unlike many other languages, you will always find multiple ways to perform the same action in Ruby. To append a new element to a given array, you can also use push method on an array. Add the string "woot" to given array by calling push.
| explanation  | push or << both work
| language     | Ruby
| start        | [1, 2, 3, 4, 5]
| solution     | [1, 2, 3, 4, 5].push("woot")
| output       | [1, 2, 3, 4, 5, "woot"]
| description  | push called on array


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

| problem type | coding                                         
|--------------|--------------------------------------------------------
| name         | indexOf practice
| statement    | use JavaScript's indexOf() to find the index of the number 4
| explanation  | the first number has an index of 0
| language     | JavaScript
| start        | [1,2,3,4,5]
| solution     | [1,2,3,4,5].indexOf(4)
| output       | 3
| description  | called indexOf()
