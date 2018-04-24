# Basic of Functional Programming

First we need to two simple functions to introduce what FP is.

```text
public func sum(a: Int, b: Int) -> Int {
    return a + b
}
```

So, the function takes an input of  `a:Int` and `b:Int`, and the output is also an Int. Clear and simple, right?

Now the second function

```text
public func doSomething() {
    let someSecretVar = SecretBox.popFirstSecretVar()
    decode(secretVar)
}
```

This one, while taking no input it also return nothing, but inside it seems like something has happened. So when we use this function as API somewhere else, we could never know what will happen if  the implementation is hidden.

Those hidden inputs and outputs are called "side-effects". It's undesired and an bad pattern.

### Why side-effects are bad?

When they work as expected they are fine. But we have to trust that the implementation will always be correct as time marches on. 

However, we can't sure if the state is always as same as the function expected. What if we change implementation of `SecretBox`? Will `func popFirstSecretVar()` still work?  We can't just pray all these side-effects still work. Further more, after large amount of side-effects compiled up, the whole world might be destroyed even we change some little part of work, even it seems total irrelevant.

So, the function has no side-effects is called "Pure Function".

### What Make a Function "Pure"?

It has to have neither hidden inputs nor hidden outputs.

### What is 'Functional Programming'?

FP is basically a way to construct our application with pure functions. And a functional programming language is one that supports and encourages programming without side-effects, help programmer eliminate side-effects wherever possible, and tightly control them wherever it's not. 

