# TypeScript 001 <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/4c/Typescript_logo_2020.svg/2048px-Typescript_logo_2020.svg.png" width="25" height="25">

_Before you get stuck in, this tutorial assumes you have at least a basic understanding of javascript. If not, I recommend you start with [This course from Codecademy](https://www.codecademy.com/learn/introduction-to-javascript)_

You love JavaScript, and you've heard of this thing called TypeScript and that lots of companies are using it, but you've no idea where to start to learn it...Welcome to **TypeScipt 001**

<!-- TOC start -->

- [Why TypeScript](#why-typescript)
  - [Once upon a time there was JavaScript](#once-upon-a-time-there-was-javascript)
  - [TypeScript to the rescue!](#typescript-to-the-rescue)
    - [The Benefits of TypeScript](#the-benefits-of-typescript)
    - [The Cons of TypeScript](#the-cons-of-typescript)
- [How do we add TypeScript Annotations?](#how-do-we-add-typescript-annotations)
  - [Primitives](#primitives)
  - [Functions](#functions)
  - [Interfaces](#interfaces)
  - [Classes????](#classes)
  - [Generics](#generics)
- [Turning TypeScript into JavaScript](#turning-typescript-into-javascript)
- [Resources??](#resources)
- [Summary??](#summary)

<!-- TOC end -->

## Why TypeScript

### Once upon a time there was JavaScript

Javascript is a great language to get started with. It has a very low barrier to entry and it's very versatile, evolving from a purely front-end language to a one stop shop, full stack language. It runs in the browser, doesn't require any complicated compilation or tooling and is interpreted line by line.

This forgiving nature, however, does increast the chances of making mistakes and creating bugs.

Consider this program:

```
function sum(a, b) {
  return a + b;
}

console.log(add(3, 4)); // 7
```

A seemmingly simple program to provide the sum of two numbers. However weird things happen if we start calling this function with values that aren't numbers.

Javascript does something called [type coercion](https://developer.mozilla.org/en-US/docs/Glossary/Type_coercion) which means it converts values from one data type to another. This can happen explicitly (meaning we'd be prepared for it) or implicitly, which can have some curious results as you'll see here when we use the above function with different arguments:

```
console.log(add(1, "4")); // 14
console.log(add(1, true)); // 2
console.log(add(1, "type")); // 1type
console.log("5" - 1); // 4 (string "5" is converted to number)
console.log("5" * "2"); // 10 (both strings are converted to numbers)
console.log(0 == false); // true (number 0 is converted to false)
console.log(0 === false); // false (no type coercion, different types)
```

<figure>
    <img src="https://media.giphy.com/media/3o7btPCcdNniyf0ArS/giphy.gif?cid=790b7611k17gjgfnwrk7053g996i08skyunjpsooiov8erfm&ep=v1_gifs_search&rid=giphy.gif&ct=g"
         alt="confused gif">
    <figcaption>This can be very confusing!</figcaption>
</figure>

### TypeScript to the rescue!

TypeScript can help us be explicit about what types we expect where. TypeScript is a superset of JavaScript, which means it is an additional layer on top of JavaScript which gives us additional type information functionaility.

TypeScript is then compiled into JavaScript that can run anywhere. It's even backwards compatible, so you can start converting a JavaScript program into TypeScript without breaking anything.

#### The Benefits of TypeScript

- Types give us the ability to catch errors in the code early, before it even runs. If you assign a value of the wrong type to a variable, you'll get an error when you try to compile.
- Types make it easier for code to be read because you're able to explicitly state what types you're expecting
- Types add predictability: Once a variable is declared as a certain data type, it will always be that data type
- Lots of IDE's support TypeScript with options for autocompletion and feedback while typing. Most will flag type-related errors as they happen.
- It supports concepts from Object Oriented Programming (OOP) like classes and interfaces, something I'll introduce a little bit of below.

#### The Cons of TypeScript

- It's another layer to learn on top of JavaScript
- It can bloat your code, you have to write a lot more to make sure you're defining types correctly
- It adds an extra transpiling step where it is converted to JavaScript (but this is so automated as to be negligible)

<figure>
    <img src="https://media.giphy.com/media/r2ipC1yfH4PoIY2wEK/giphy.gif?cid=790b761178o11xbvz4yx63yjx31ycdfdthjuyeqqq8bafinv&ep=v1_gifs_search&rid=giphy.gif&ct=g"
         alt="Rescue Rangers to the Rescue">
    <figcaption>A successful rescue!</figcaption>
</figure>

## Types of Types

### Primitives

There are three common [primitives](https://developer.mozilla.org/en-US/docs/Glossary/Primitive) in Javascript: `string`, `number`, `boolean`

- `string` is for string values like "This. Is. TypeScript!"
- `number` is for any number like `42`
- `boolean` is for `true` or `false`

### Arrays

You can specifiy the type of an array by stating it as an array of types. For example, and array of strings like `["What", "Three", "Words"]` could by typed using this syntax: `string[]`. It could also be written as: `Array<string>`, but don't worry about this yet, we'll cover it in the [generics](#generics) section.

### Any

TypeScript also has a special type, `any`, that can be used when you want to avoid typechecking errors for a specific value or you have an array that can contain a variety of types.

Sometimes when you don't specify a type, and TypeScript can't infer the type from what you've written, it will default to `any`. You want to **avoid** this because `any` isn't typechecked. You can use the compiler flag `noImplicitAny` to highlight any `any`'s as an error...

## How do we add TypeScript Annotations?

You add a type annotation in TypeScript by appending a colon (`:`) followed the type after that variable name, function parameter or function.

A simple example would be something like this:

```
const num = 1; // JavaScript
const num: number = 1; // TypeScript
```

Assigning Types can be more complicated, but in essense this is how you would do it. TypeScript is also smart enough that it can figure some of the types in your program based on the information you've given it. This is called "type inference"

### Functions

TypeScript allows you to specify the types of both the input and output values of a function.

#### Parameter Type Annotations

You can add type annotations after each parameter in a function when you declare it, which will mean the arguments to that function will be checked. For example:

```
function sayYourName(name: string) {
    console.log(`OK, my name is ${name}`)
}
```

#### Type Annotating the Return value

You can also make sure your function is returning a specific type, this would be written like this:

```
function getFavouriteFood(): string {
    return "chicken";
}
```

If the function isn't returning anything (for example just setting a value in a variable), the type would be `void`

#### Both at once

Combined (input and output) would look like this, using the first example

```
function sayYourName(name: string): string {
    console.log(`OK, my name is ${name}`)
}
```

### Interfaces

Interfaces allow you to create your own custom types. For example how would you enforce type checking on `objects` in your code? An interface!

The syntax goes something like this:

```
interface NameOfObject {
    key: type;
}
```

An example for a Pet object which has a name, age, and animaltype:

```
interface Pet {
    name: string;
    age: number;
    animalType: string;
}
```

You'll notice it's named using a capital letter, this is important to distinguish it as a custom type.

### Generics

Sometimes you might want a function to be able to work with lots of different types. You could make this work by writing lots of functions to cover all the types, but this is time consuming and repititive and messy. In comes `generics` to make our code more flexible and reusable.

Let's take a super simple example where you want to input a value and get that same value out, but it could be any type, and you don't want to lose the inforamtion about what types are being used.

First we need to write a **Generic Function**

```
function returnAThing<Type>(value: Type): Type {
    return value;
}
```

`Type` here is a placeholder, and you can call it anything you'd like and it represents the type you want the function to work with.

When you call the function, you can specify the type explicitly like so:

```
let number = returnAThing<number>(99); //number is of type number
let sentence = returnAThing<string>("This is a lot of text"); // sentence is of type string
```

Or TypeScript can infer it for you:

```
let number = returnAThing(99); // TypeScript infers this is a number
let sentence = returnAThing("This is a lot of text"); // TypeScript infers this is a string
```

Generics give you a lot of flexibility without sacrificing type safety and makes your code more reuasable.

## Turning TypeScript into JavaScript

As mentioned somewhere far above, you need to `transpile` TypeScript into JavaScript for it to be used.

If you're using `Node` you will need to add the `typescript` package and run the `tsc` compiler tool
However frameworks like `Vite` and `Next` does the compilation for your transparently in the background, so no extra legwork required.

## Resources

Here are some useful links if you'd like to delve into TypeScript in more detail.

[TypeScript in 5 minutes](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)

[The TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)

[Net Ninja Youtube Playlist](https://www.youtube.com/watch?v=2pZmKW9-I_k&list=PL4cUxeGkcC9gUgr39Q_yD6v-bSyMwKPUI)

[TypeScript Playground](https://www.typescriptlang.org/play/?#code/PTAEHUFMBsGMHsC2lQBd5oBYoCoE8AHSAZVgCcBLA1UABWgEM8BzM+AVwDsATAGiwoBnUENANQAd0gAjQRVSQAUCEmYKsTKGYUAbpGF4OY0BoadYKdJMoL+gzAzIoz3UNEiPOofEVKVqAHSKymAAmkYI7NCuqGqcANag8ABmIjQUXrFOKBJMggBcISGgoAC0oACCbvCwDKgU8JkY7p7ehCTkVDQS2E6gnPCxGcwmZqDSTgzxxWWVoASMFmgYkAAeRJTInN3ymj4d-jSCeNsMq-wuoPaOltigAKoASgAywhK7SbGQZIIz5VWCFzSeCrZagNYbChbHaxUDcCjJZLfSDbExIAgUdxkUBIursJzCFJtXydajBBCcQQ0MwAUVWDEQC0gADVHBQGNJ3KAALygABEAAkYNAMOB4GRonzFBTBPB3AERcwABS0+mM9ysygc9wASmCKhwzQ8ZC8iHFzmB7BoXzcZmY7AYzEg-Fg0HUiQ58D0Ii8fLpDKZgj5SWxfPADlQAHJhAA5SASPlBFQAeS+ZHegmdWkgR1QjgUrmkeFATjNOmGWH0KAQiGhwkuNok4uiIgMHGxCyYrA4PCCxQAQvA5R5OIp3OlBABJVA4MjsFC81BzyAAbjHOdb04AYgxoJn8uMhy0vIvl2vilTKJxmMFx2lBBViEuK7yw+LuPWeFdUOxEXy13e8gPjgxBPlezAHpeL78gAsuakjvp+rhUr+yT-vqYCcOwiDSN8t4bgwMbYbh2K8gAHABBEDGmRE4d8B5YXRpGgAAnOeKhjI4ZBMEkqTAsOZjCEqcSoAemCoKgBAFCAEiyQEqDtIIpKoIw14BOKzDANwNSCMADg8Px8TAAATMAkB6GQeDcEwpQKUQggBOJiDQAAxFxeR6uuND8cewi8gA2ku878Mku6ZvwQVZpFAC6lHeUeI6CCBB4+SO-nRTyoCBcuEU5TiYWQLFGFiF47nFkSjEkb8Xn9MR3x+VlACM-DGfwADMbX8AALPwACs-AAGxFXelX1cltVMelmX+c1oCtaAnWgD1oD9aAA38AA7EVxScWQ3HlakUHXtVd5HcwDX+XyDB8vwfLSHyw0bmdSXEJBz7XlNAVXTd-L3dtKiCNhOJcLA9SNMEyQg2DXiA4gSqMY1DF1WQ-CMcZSNMTqoAAN6KCUJR3ugebQBjJGZQjoAANQTcZa74yWOb4k0xOKAAvsVAAikCujcxicPGaDtFgdRwvonS4Z+STSAAVtzqCKBkChkKFSwAMLYLA8QcDQuP0wyPaiRNJF0-jXAUAAjvOk7cG94EmyUQism6NuHgJnD22I3DcASgjPBk+i28M6VruzxRczzfTiPzEiC0QYhugwwicAykCuKrcrtqo6iaKIkC7PR-L9s89w0sG4r8qENLPM8ybgFKdkoOnIr4plfJFyXwYAD4V1XNd1+egFTqg-bQPOyZkKEwrwBIB5N5nr7t6XK5AA)

## Summary

In short, while TypeScript can seem a little daunting at the beginning, if you work through it iteratively, you'll find the extra time writing and learning will reap rewards further down the line in terms of fewer bugs, more security and more readable code!
