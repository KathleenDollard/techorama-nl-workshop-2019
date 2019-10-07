# Techorama Netherlands Workshop

These materials are provided as is without any warranty.

Thank you for joining me in my workshop!!

(If you weren't in the workshop, these materials probably won't make much sense)

- Materials
- Clarifying Async question
- Summary at end (your recollections): Summary.txt

Let me know if I missed anything. 

## Materials

The slide decks are in this repo. The order is:

Morning: 
* IntroFuture.pptx
* TypesEtc.pptx

Afternoon:
* Async.pptx
* What's New in C#8.pptx


I decided to leave these in their own repos:

- [C# 8 - done](https://github.com/KathleenDollard/sample-csharp-8/tree/techorama-nullable-done) and [C# 8 - start](https://github.com/KathleenDollard/sample-csharp-8/tree/start-working)
- [Puzzles](https://github.com/KathleenDollard/sample-puzzles/tree/working-techorama) - working-techorama branch
- [Async WinForms sample](https://github.com/KathleenDollard/sample-async-simple-desktop) - main branch


## Clarifying Async question

In the Async section of the talk, Niek de Gooijer pointed out an important point. To show this with an example: Assume `SlowOp2` takes 2 seconds and `SlowOp1` takes 1 second. Each is an async method that returns a `Task`. 

When the methods are called in sequence, the second operation does not start until the first is completes, and the combined operations take 3 seconds. 

```C#
await SlowOp2();
await SlowOp1();
```

If instead, the `Task`s are collected prior to any await, both operations start at the same time and the operation completes in two seconds. The `Task` represented in `task1` is already complete when the first is finished. If the order of the `await`s was reversed, it would still take 2 seconds. 

```C#
var task2 = SlowOp2();
var task1 = SlowOp1();
await task2;
await task1;
```

