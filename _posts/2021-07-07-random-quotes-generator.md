---
layout: post
title: 'A Random Quote Generator for Your Terminal'
date: 2021-07-07 21:37:00 -0400
featured-img: /img/post-images/random-quotes-generator/my-terminal.png
# categories: [Flatiron School]
tags: []
excerpt: <p>What if you had an inspirational quote to greet you every time you opened a new terminal? Now you can! Plus, you can customize the list of quotes your random quote generator pulls from! Read on for a step-by-step guide on how to implement this simple script in your terminal setup.</p>
---

I'm a member of this amazing online community called [Virtual Coffee](https://virtualcoffee.io/). We meet twice a week and have conversations about the tech industry as well as tech-adjcent topics. In today's meeting, we kept coming back to reducing project anxiety by breaking large tasks down into several smaller ones. It reminded me of a quote I revisit often when I feel overwhelmed:

> _The person who removes a mountain begins by carrying away small stones. —Chinese Proverb_

In fact, I have a whole file filled with quotes I pick up here and there that bring me joy and inspiration. I’ve created a bash script which outputs one quote at random from this file every time I start up a new terminal session. After sharing this with my Virtual Coffee group, they were eager to learn how I did it, so here's a step-by-step write up for you to create a random quote generator of your own!

## The Script

Add the following `quote` function to your <span class="bold teal">.bash_profile<span> file and call it just above the line where you define `export PS1`:

```bash
function quote {
  # Set the file path to the quotes file
  quote_file=$HOME/Development/code/quotes.txt
  # Retrieve a random quote for the file
  sed -n $(awk "END{ print $RANDOM%NR+1}" $quote_file)p $quote_file
}

# This function builds your prompt. It is called below:
function prompt {

  # Call the quote function inside your prompt function and it prints a quote to your terminal
  quote

  # Here is where we actually export the PS1 variable which stores the text for your prompt
  export PS1
}

# Call the prompt function
prompt
```

If you don't have a `prompt` function defined where you export your `PS1` variable, you should do so. This allows your quote to be printed out just before your regular bash prompt.

![My terminal prompt](/img/post-images/random-quotes-generator/my-terminal.png)

## A Breakdown of the Above

The `quote_file` variable is a path to the simple text file where my list of quotes are stored. Depending on your editor (I use Mac’s default, TextEdit), the quotes may wrap. That’s okay as long as you start each new quote on a separate line.

**Edge Case:** Leave a blank new line at the end of your text file. If the last quote in your file is randomly selected, the `PS1` in your terminal will appear on the same line directly after the quote if you don't do this!

This snippet `awk "END{ print $RANDOM%NR+1}" $quote_file` is actually using the [AWK scripting language](https://en.wikipedia.org/wiki/AWK)! This denotes that we're executing the action `{ print $RANDOM%NR+1}` for the pattern `END` on the file represented by the variable `$quote_file` (as defined on the line above it). `END` counts the number of lines in the entire `$quote_file` document. Then `NR` returns the specified row number, which in this case is that of the last line as denoted by `END`, and the result of `$RANDOM%NR+1` is printed out. `$RANDOM` is a built-in bash variable that returns a random integer, which we use as the numberator to `NR`'s denominator to return a remainder using the [modulo operation (`%`)](https://en.wikipedia.org/wiki/Modulo_operation).

**Edge Case:** After the remainder is calculated, we increment by one. Doing this accounts for a remainder of zero and ensures that a quote will always be returned.

Do you see how that whole code snippet is encapsulated in `$()`? Let’s take the number we just returned and assign it to the variable `modulo` for the rest of this breakdown.

Now what we’re left with is `sed -n $(modulo)p $quote_file`. `sed` isn’t bash—[`sed` is actually a Unix utility called a stream editor](https://en.wikipedia.org/wiki/Sed)! And like AWK, we can pass it options before passing the input file. By default, `sed` prints out all processed input so we use `-n` to suppress output and `p` to print specific lines. We already know from above that `modulo` is a random number that maps to the number of lines in your quote text file, therefore, you should see a random quote from your file print to the terminal!

I also have a pretty little bash prompt that shows me where I am in my directory, has custom colors, and displays git repos and branches. If you want to know more about this setup, DM me on Twitter [@meg_gutshall](https://twitter.com/meg_gutshall)!
