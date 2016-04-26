# Swift — Functions

## Objectives

1. Distinguish the functional and object-oriented programming paradigms.
2. Learn how functions and methods differ conceptually
3. Create and call simple custom functions in Swift.
4. Create and call custom functions that provide a return.
5. Create and call custom functions that take arguments.
6. Recognize some of the errors common to developing custom functions.

## Introduction

As a language, Swift blends the programming paradigms of [Object-Oriented Programming (OOP)](https://en.wikipedia.org/wiki/Object-oriented_programming) with many elements of [functional programming](https://en.wikipedia.org/wiki/Functional_programming). This approach is more like dynamic programming languages like Ruby and Python which blend the paradigms also.

### Functions vs. Methods

In contrast to Objective-C, Swift permits functions that are not associated with a class (i.e., they are standalone). This is the philosophical distinction between methods and functions: methods are attached to a class, and functions stand alone. In Swift, the syntax for either is identical—with the exception that methods are associated with a particular class and have various options for visibility, etc. We'll discuss methods in more detail in later lessons.

Standalone functions are available globally, meaning that they can be called from anywhere in a project which contains them.

Take for example the `print()` function that we've already introduced and had you use. It's a function which sends its string argument to the Debug Console. It's defined once in the Swift Foundation library and available anywhere that the Swift Foundation is imported (which will generally be *everywhere* in a Swift project).

```swift
print("Heyyy, iOS!")
```
This will print: `Heyyy, iOS!`.

## Creating a Custom Function

Function declarations follow this full syntax form:

```swift
func nameOfFunctionArgument1(argument1: Type1, argument2: Type2) -> ReturnType {
    // implementation
}
```
We're going to work up to this, starting with a simple function that takes no arguments and provides no return.

### Simple Functions

Let's write a function that we can reuse anywhere to remind ourselves to walk around every once in a while. We're just going to have it define the simple behavior or printing a string that reads "Take a walk!".

We'll need to start with the keyword `func` that tells the compiler we'll be defining a new function starting on this line.

```swift
func
```
Then we'll need to give our function a name, ending with a set of empty parentheses which signifies that our function takes no arguments (a.k.a. parameters), and opens the curly braces which defines the body of the function's implementation:

```swift
func printTakeAWalk() {

}
```
**Top-tip:** *When writing a function which takes no arguments, do not forget the trailing parentheses. Is is a required part of Swift's function syntax and cannot be omitted.*

Now we're going to define the behavior that we want the function to perform, which is to print "Take a walk!":

```swift
func printTakeAWalk() {
    print("Take a walk!")
}
```
Great! Now we can remind ourselves to stay active.

##### Calling A Simple Function

To call our custom function which takes no arguments, we simply type the name of the function on a new line:

```swift
func printTakeAWalk() {
    print("Take a walk!")
}
printTakeAWalk()
```
This will print `Take a walk!` just like we told it to.

We can call it a second time to reuse our code:

```swift
func printTakeAWalk() {
    print("Take a walk!")
}
printTakeAWalk()
printTakeAWalk()
```
However, we *cannot* call our function *before* its definition in the file that contains it:

```swift
printTakeAWalk()  // error
func printTakeAWalk() {
    print("Take a walk!")
}
printTakeAWalk()
printTakeAWalk()
```
This produces an error that reads `Use of unresolved identifier 'printTakeAWalk'`:

![](https://curriculum-content.s3.amazonaws.com/swift/swift-functions/error_use_of_unresolved_identifier.png)

### Functions With A Return Type

Functions which don't provide a return are somewhat rare, so let's write a function that returns something. Let's standardize a greeting for the iOS class that goes "Heyyy, iOS!". Our function should simply return a string containing this value.

Let's start our new custom function just like we did before, using a different name:

```swift
func heyIOS()
```
But this time let's define it with a return type of `String`. After the closing parenthesis which encapsulates the (in this case, absent) arguments, we insert a right arrow `->` and the name of the type (in this case, `String`), followed by the opening curly brace:

```swift
func heyIOS() -> String {

}
```
Now that we have our function opened, we can use the `return` keyword to pass back a string with our greeting in it:

```swift
func heyIOS() -> String {
    return "Heyyy, iOS!"
}
```
Great! Now we can access our standard greeting from anywhere in our code.

#### Capturing A Function's Return

We can capture our function's return into a variable by using `let` or `var` and the assignment operator `=`:

```swift
let greeting = heyIOS()
```
The instance `greeting` will now hold the string value `Heyyy, iOS!`, and be implicitly typed to match the function's return type (in this case, `String`).

We can then print this instance as normal:

```swift
print(greeting)
```
Or we can nest the function call by passing it directly into a another function's arguments, such as in printing the return of `heyIOS()` directly:

```swift
print(heyIOS())
```
Both of these will print: `Heyyy, iOS!`.

##### Namespace Errors

It's important to note that attempting to use a function's name to name a variable will produce an error. If we attempt to capture the return of `heyIOS()` into a variable named `heyIOS`, the compiler will complain:

```swift
func heyIOS() -> String {
    return "Heyyy, iOS!"
}
let heyIOS = heyIOS()  // error
``` 
![](https://curriculum-content.s3.amazonaws.com/swift/swift-functions/error_variable_used_within_its_own_initial_value.png)

So instead we have to name our variable something else such as `greeting` like we did above.

### Functions With One Argument (a.k.a Parameter)

To write a custom function which takes a single a argument, we're going to follow the syntax:

```swift
func aFunctionThatDoesSomethingWithAThing(argument1: Type1) -> ReturnType {
    // implementation
}
```
The argument's name inside the parenthesis defines the name of that argument inside the scope of the function. So, in the function above, we would refer to the first argument as `argument1` when implementing the function.

Let's write a dynamic version of our `heyIOS()` function that takes an argument for who we're greeting. Let's call our new function `heyGroup()` and name its string argument `group`:

```swift
func heyGroup(group: String) -> String {

}
```
Since it returns a string, let's interpolate the argument string into the return instance:

```swift
func heyGroup(group: String) -> String {
    return "Heyyy, \(group)!"
}
```
Note that the group is referred to as `group` inside the function body.


#### Calling A Single-Argument Function

Now we can use our function to generate a special salutation for any group that we wish to greet. We need to pass it a string argument, so let's start with our "iOS" group to make sure it works:

```swift
let greetIOS = heyGroup("iOS")
```
The `greetIOS` instance will hold the value `"Heyyy, iOS!"`.

We could also pass the function's return directly to the `print()` function:

```swift
print(heyGroup("iOS"))
```
This will print: `Heyyy, iOS!`.

Perfect! If we pass it a different string argument it should change accordingly:

```swift
let greetWeb = heyGroup("Web")
let greetEveryone = heyGroup("everyone")
```
The `greetWeb` instance will hold the value `"Heyyy, Web!"`.  
The `greetEveryone` instance will hold `"Heyyy, everyone!"`.

##### Argument Type Error

But what happens if we try passing our function an argument that doesn't match the expected type?

```swift
let greetValjean = heyGroup(24601)  // error
```
We get an error reading `Cannot convert value of type 'Int' to expected argument type 'String'`. Oops!

![](https://curriculum-content.s3.amazonaws.com/swift/swift-functions/error_cannot_convert_value_to_expected_argument_type.png)

However, if we convert the argument to the correct type, the compiler will accept it:

```swift
let greetValjean = heyGroup("24601")  // accepted
```

### Functions With Two Arguments

Now we're ready to unpack the full syntax from the beginning of this lesson:

```swift
func nameOfFunction(argument1: Type1, argument2: Type2) -> ReturnType {
    // implementation
}
```
Inside the parenthesis, additional arguments are listed by `name: Type` separated by commas. The name of the function should reflect the meaning of the first argument. The names of all additional arguments are part of the function-calling syntax:

```swift
let capture = nameOfFunction(<value>, argument2: <value>)
```
Let's create a new function that takes two arguments, one for the group, and for a speaker who's come to talk to the students, and return a string containing a message to tell the students:

```swift
func heyListenGroup(group: String, speaker: String) -> String {
    return "Heyyy, \(group)! Come listen to \(speaker) give a talk."
}
```
Note that the first part of the function name, `heyListenGroup`, contains a hint as to the meaning of the first argument -- it is a group. There is a second string argument for `speaker` listed inside the parenthesis, and it is later used in string interpolation.

Calling our function would look like this:

```swift
let listenToJoe = heyListenGroup("iOS", speaker: "Joe")
```
The variable `listenToJoe` will now hold the value `"Heyyy, iOS! Come listen to Joe give a talk."`.

Notice how the second argument is named in the function call? Each argument is ideally preceded by a label that indicates its purpose. The first argument, `"iOS"`, is implied to be a group by `heyListenGroup`. Subsequent arguments are prefixed with their names from the function definition -- in this case, `speaker:` preceds the actual argument value, `"Joe"`, thus indicating that argument is a speaker's name.

### Functions With Many Arguments

Functions which take more than two arguments follow this same syntax. To show an example, let's write a new function that also tells the students how long in minutes the speaker will talk. We'll need to define our function with a third argument `minutes` that takes an integer:

```swift
func heyListenGroup(group: String, speaker: String, minutes: Int) -> String {
    return "Heyyy, \(group)!" Come listen to \(speaker) give a talk for \(minutes) minutes."
}
```
We can then call our function in a similar way, passing in a value of the correct type for each argument:

```swift
let listenToOrta = heyListenGroup("everyone", speaker: "Orta", minutes: 60)
```
The variable `listenToOrta` will hold the value `"Heyyy, everyone!" Come listen to Orta give a talk for 60 minutes."`.

Did you notice that we wrote a completely separate function with the same base name `heyListenGroup` and yet the compiler never complained? The compiler differentiates it by the arguments it takes. Objective-C developers will find this familiar because the names of the arguments are seen as part of the function's name.

![](https://curriculum-content.s3.amazonaws.com/swift/swift-functions/autocomplete_functions_distinguished_by_parameters.png
)

## Reference Link

For Apple's documentation of Swift functions, review the [Functions](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Functions.html#//apple_ref/doc/uid/TP40014097-CH10-ID158) chapter of *The Swift Programming Language*.

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/swift-functions' title='Swift Functions'>Swift Functions</a>  on Learn.co and start learning to code for free.</p>

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/swift-functions'>Functions</a> on Learn.co and start learning to code for free.</p>
