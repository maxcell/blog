---
layout: post
title: Day 1 - Inverse Captcha
date: 2017-12-01
image: /blog/assets/christmas.png
---

Howdy there! Welcome to my first writeup for solutions to Advent of Code. If you don't know what that is, [Advent Of Code](http://adventofcode.com) is an annual coding event started by [Eric Watsl](https://twitter.com/ericwastl) where every day in December leading up to Christmas has a new challenge. The idea of the Advent of Code is to encourage people to have some fun. Some people use this to learn new programming languages, some use it to grow in their current language, others compete with their friends in private leaderboards. Whatever the case may be, [sign up and let's work together](http://adventofcode.com/2017/auth/login)!

Today, we are going to talk about my solutions to the problems from [Day 1 - Inverse Captcha](https://adventofcode.com/2017/day/1). If you haven't read it, I highly encourage you do! The TL;DR (Too Long; Didn't Read) of it is that one of Santa's elves needs your help making the printer work by sending us into it and solving a puzzle so fast it will think we aren't human, a [captcha](https://en.wikipedia.org/wiki/CAPTCHA).

For many of the problems in Advent of Code, you will more than likely need to figure out how you will take inputs for your program. I tend to read a file in and go from there. I won't share that boring detail. Here's ultimately what we need to do: "The captcha requires you to review a sequence of digits (your puzzle input) and find the sum of all digits that match the next digit in the list. The list is circular, so the digit after the last digit is the first digit in the list."

Here are the examples we were given:
- `1122` produces a sum of `3` (`1` + `2`) because the first digit (`1`) matches the second digit and the third digit (`2`) matches the fourth digit.
- `1111` produces `4` because each digit (all `1`) matches the next.
- `1234` produces `0` because no digit matches the next.
- `91212129` produces `9` because the only digit that matches the next one is the last digit, `9`.

So let's think about this for a second. We know we start from the beginning and we don't just stop at the last digit of our number. We have to continue *around and back* to the first digit. You could think of it as a dog chasing their tail! As it said in the problem, we describe things that connect from head to tail as being "circular". So if we put each of the digits into their own box and then drew arrows connecting it, we would have one last arrow from the last digit back to our first.

<img src='{{ site.baseurl}}/assets/img/process.png' asset="@magick:2x" alt="Diagram showing each step to the process. Arrows connecting consecutive digits and checks indicating success in the first and third check and xs for failure in second and four (final) step">

While we are doing that, we are going to be adding them together to a sum which I just happened to call `total` because of the fact that Python already has a function called `sum()`. Also so you know, `data` represents the input line still as a string so when you see doing `int(data)`, this is me converting it to an integer. First, I considered iterating around as such:

```python
def sum_of_cons(data):
  total = 0
  for i in range(len(data)):
    ...

  return total
```

This at least solves our problem by how we are going to go move one digit at a time. However, we have to check if the digit we are looking at currently (in this case we designated it as `i`) is the same value as the following it (after `i` would be `i + 1`). If the two are the same, we want to add our value to our running `total`. So we can add that code underneath our for loop:

```python
def sum_of_cons(data):
  total = 0
  for i in range(len(data)):
    if data[i] == data[(i + 1)]:
      total += int(data[i])

  return total
```

However, there is still a missing piece to this! We said we have to go around to the front and check if the last digit and first digit match up. Otherwise, when we hit the final iteration, Python will throw an error and say we have hit an Array Out of Bounds exception.

There are probably a few ways you could come up with a solution for this. But here is a neat little piece of information that may help you in your programming journey! Let's say we had this set of numbers (`1122`) repeating cforever so you'd have `112211221122...`. Well we know we repeat again after our length of our current string which happens to be `4`. So when we hit the fifth index, we have managed to find the first index of our original string. This would be true if we did the same thing with the 9th index too. So this means any multiple of our string length `+ 1` will be the first digit. To remove any multiple, we could use the `%` or modulus operator. Let's says we had the number `8` (the ninth index) and we were to modulus it by `4`  (the length of our string). It would give us back the **remainder** of when we took out all of the possible multiples of 4 we could have that would leave the result as a whole number. If that still is a bit hard to understand, `%` looks a lot like the `/` and that's because it instead of telling you how many multiple something can go into another number, it will tell us the remainder. These are two peas in a pod!

We can use this trick to say when we hit our last value for our `for` loop. Given our string `1122`, the last iteration would be at `i = 3` therefore `i + 1 = 4`. Now we wil update our `if` with checking the modulus (`%`) of the index location of our following digit (`i + 1`), we see the result would check if `data[3]` and `data[0]` are equal. This is because `4 % 4 = 0`. `4` divides evenly into `4` with no remainder `0`.

So let's update the code with our final change:

```python
def sum_of_cons(data):
  total = 0
  for i in range(len(data)):
    if data[i] == data[(i + 1) % len(data)]:
      total += int(data[i])

  return total
```

Viola, we have solved the first problem! Great work! Now let's tackle the second part of day 1. This time it says instead of it circling back to the beginning, we have it going halfway around the list. Also don't worry, our inputs will always be even so there is always a length that is evenly divisble.

This means is instead of having to check for the consecutive (`i+1`), we will change the `1` to be the midpoint of our list. We take the total length and divide it in half `len(data)/2` and add that to `i`. Since we are still wrapping around our list, we again need to use the modulus operator! So we only really changed one spot in this function by replacing our `1` with `len(data) / 2`:

```python
def sum_of_mid(data):
  total = 0
  for i in range(len(data)):
    if data[i] == data[(i + (len(data)/2)) % len(data)]:
      total += int(data[i])

  return total
```

And there you have it! Solutions to both problems! If you found this helpful or you want to share your own solution, reach out to me on [Twitter](https://twitter.com/maxcell)! I'd love to hear it. If you happen to notice a bug in any of code snippets or a typo/mispelling, feel free to head over to my GitHub and you can open a PR onto [my blog](https://github.com/maxcell/blog) and I'll review it. Good luck with the rest of the Advent of Code!
