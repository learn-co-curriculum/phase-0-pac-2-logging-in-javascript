# Logging in JavaScript

## Learning Goals

- Learn about logging in JavaScript
- Use `console.log()` in the development process
- Use `console.log()` for debugging

## Logging

The venerable `console.log()` is an all-purpose logging _method_. (A **method**
or a **function** is a bit of code that _does_ something. We _call_ them when we
want them to act.) In programming, _logging_ refers to the process of printing
information about the program as it runs. Note that `console.log()` is a
_development_ tool; it's not something that's used in deployed code.

Let's take a look at how it works. Open up [replit][] and follow along.

As we've seen before, there is an example provided in the code window:

```js
console.log("Hello, world!");
```

We've also seen that we can log more than just a simple message. In fact, we can
pass any number of messages to `console.log()` by separating them with commas;
when printed, they'll be separated by a space:

```js
console.log("one", "two", "three");
```

We can also include values of different types. Give this a try:

```js
console.log("I must have logged", 1000, "times today.");
```

Note that, for that first string ("I must have logged"), the comma is _after_
the end quotation mark. This is because the comma is not part of the string;
instead, it's how we tell JavaScript, "Hey, I'm going to give you something
else!"

As we saw earlier in this section, we can also pass _variables_ to
`console.log()`:

```js
const name = "Spinach the Shiba";
console.log("Hello,", name);
```

As a reminder, we can log any _expression_ — even very complex ones — using
`console.log()`.

## Using `console.log()` in the Development Process

Where `console.log()` gets really helpful is when you use it to check that your
code is functioning as you want it to. Let's revisit an example from an earlier
lesson:

```js
const age = 20;

let isAdult=false, canWork=false, canEnlist=false, canDrink=false;

if (age >= 21) {
  canWork = true;
  canEnlist = true;
  isAdult = true;
  canDrink = true;
} else if (age >= 18) {
  canWork = true;
  canEnlist = true;
  isAdult = true;
} else if (age >= 16) {
  canWork = true;
}
```

Let's say we want to run some tests to make sure that we have our `if` statement
set up properly. We can do this by checking the values of the four variables for
different values of `age`. Here's where `console.log()` comes in.

Go ahead and open [replit][] and copy/paste the code above into the code window.
Next, let's add the following to the end of our code:

```js
console.log(canWork, canEnlist, isAdult, canDrink);
```

Next, let's set the `age` variable to a value of 16 and click the run button.
You should see the following output to the terminal:

```console
true false false false
```

It looks like our code is working if `age` is set to 16, but our message could
be a little more informative. We can see that only one of the variables is
`true`, which is what we want, but it's not immediately apparent _which_ of the
variables is the one that's `true`. So let's add some labels. To do this, we'll
use a combination of strings and variables inside our `console.log()`. While
we're at it, let's log the `age` value as well. Replace the existing
`console.log()` with the following:

```js
console.log(
  "Age:",
  age,
  "Can work:",
  canWork,
  "Can enlist:",
  canEnlist,
  "Is a legal adult:",
  isAdult,
  "Can drink:",
  canDrink
);
```

This looks complicated, but all we're doing here is stringing together a series
of expressions — some of them simple string values, and some of them variables —
with commas between each one.

Alternatively, we can use string interpolation inside our `console.log()` to do
the same thing:

```js
console.log(
  `Age: ${age}, Can work: ${canWork}, Can enlist: ${canEnlist}, Is a legal adult: ${isAdult}, Can drink: ${canDrink}`
);
```

With this approach, we're passing _a single expression_ to `console.log()`
instead of a series of them. The commas here, therefore, are part of the string.
Be sure to run both versions in the REPL so you can see the difference.

If we were writing user-facing code here, we would probably want to make it
easier to read by putting each variable on its own line. We could do that either
by using multiple `console.log()`s, or by using the new line character (`\n`).
But since the `console.log()` is just for our (the developer's) use, the above
may be perfectly acceptable.

With this `console.log()` set up we can try our code with as many age values as
we like, checking each time to verify that the variables have been set
correctly.

## Using `console.log()` for Debugging

Let's say we've gotten our code to this point:

```js
const age = 18;

let isAdult=false, canWork=false, canEnlist=false, canDrink=false;

if (age >= 21) {
  canWork = true;
  canEnlist = true;
  isAdult = true;
  canDrink = true;
} else if (age > 18) {
  canWork = true;
  canEnlist = true;
  isAdult = true;
} else if (age >= 16) {
  canWork = true;
}

console.log(`Age: ${age}\nCan work: ${canWork}\nCan enlist: ${canEnlist}\nIs a legal adult: ${isAdult}\nCan drink: ${canDrink}`);
```

We have our `console.log()` set up and we're ready to start testing it. We
decide to start with our 'least adult' category, which is children under age 16,
so we set `age` equal to 15 and click run. Everything looks fine — we get four
`false`s — so we change `age` to 16, then 17. So far, so good. But then when we
test it for an `age` of 18, we see the following:

```console
Age: 18
Can work: true
Can enlist: false
Is a legal adult: false
Can drink: false
```

Hmm, obviously we've got an error somewhere. The code for ages 18-20 isn't
returning the expected result, so let's take a look at that conditional:
`else if (age > 18)`. With a simple condition like this, we might realize right
away that we accidentally used `>` instead of `>=`. But imagine a case where our
condition is more complex and we don't immediately see the problem. Let's think
about some ideas for ways we can use `console.log()` to help us find and correct
it. Be sure to follow along in the REPL.

To start, we could try logging a message _inside_ the block for the condition
where the error is (i.e., inside the block that _should_ be executing):

```js
const age = 18;

let isAdult=false, canWork=false, canEnlist=false, canDrink=false;

if (age >= 21) {
  canWork = true;
  canEnlist = true;
  isAdult = true;
  canDrink = true;
} else if (age > 18) {
  console.log("The condition returned true")
  canWork = true;
  canEnlist = true;
  isAdult = true;
} else if (age >= 16) {
  canWork = true;
}

console.log(`Age: ${age}\nCan work: ${canWork}\nCan enlist: ${canEnlist}\nIs a legal adult: ${isAdult}\nCan drink: ${canDrink}`);
```

If we click the Run button, the message does _not_ get logged so we know the
code block is not getting executed. This tells us that there's something wrong
with the conditional itself. If the message _did_ get logged we would know that
the problem is somewhere inside the code block instead.

Next, we could try changing `age` to 19. In this case, the message _does_ get
logged, so we know our conditional is only broken for age 18. This gives us
another clue as to how to fix it.

If we had a more complicated conditional and still couldn't find the problem, we
could try logging the conditional itself, simplifying it one step at a time
until it _does_ return `true`. As soon as we get a `true` return value, we know
that the last thing we removed was what was causing the problem. For example, if
our overall condition is comprised of two conditions joined by `&&`, we could
check each expression individually. Whichever one returns `false` instead of
`true` is the one with the problem. We could then continue to "drill down" as
necessary until we find what's wrong.

> **Top Tip**: Even better, we can use `console.log()` as we're building the
> conditional in the first place, using an approach like the one outlined below.
> Only after you have the conditions working the way you need them to would you
> begin building out the code blocks. Taking this incremental approach will make
> it much easier to find and fix any errors.
>
> ```js
> if (condition1) {
>   console.log("Condition 1 returned true");
> } else if (condition2) {
>   console.log("Condition 2 returned true");
> }
> ```

You should think of the ideas presented above as examples of a general approach
to debugging. Debugging is largely a matter of using _logic_ to narrow in on the
problematic bit of code until you find the error. It is worth getting
comfortable using `console.log()` because it can be a valuable tool in this
process.

## Conclusion

In this lesson, we've learned how to use the `console.log()` method. We've also
explored some ways we can use it to help us with writing and debugging code.

[replit]: https://replit.com/languages/javascript
