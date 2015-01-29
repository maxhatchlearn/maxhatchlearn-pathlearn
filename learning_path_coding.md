Coding Exercises
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
| name         | gsub practice
| statement    | use replace to replace the l's in hello with z's
| explanation  | .replace(/l/g, "z") replaces every instace of l with z
| language     | JavaScript
| start        | "hello"
| solution     | "hello".replace(/l/g, "z")
| output       | "hezzo"
| description  | replaced l with z
