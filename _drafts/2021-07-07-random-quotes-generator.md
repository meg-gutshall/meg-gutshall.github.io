---
layout: post
title: "Open Your Terminal and Be Greeted with a Random Quote"
date: 2021-10-17 23:37:00 -0400
featured-img: /img/post-images/random-quotes-generator/my-terminal.png
# categories: [Flatiron School]
tags: []
excerpt: <p>What if you had an inspiration quote to greet you every time you open a new terminal? Now you can—and you can customize the list of quotes your random quote generator pulls from! Read on for a step-by-step guide on how to create your own.</p>
---

Hey everyone! While talking about the back pocket topic today, we kept coming back to reducing project anxiety by breaking large tasks down into several smaller ones. I thought of a quote I like that illustrates this:
“The person who removes a mountain begins by carrying away small stones.” —Chinese Proverb

In fact, I have a whole file of quotes and I’ve created a bash script that outputs one quote at random every time I open a new terminal! Add the following code inside the prompt function in your .bash_profile, just above the line where you define export PS1:
quote=$HOME/Development/code/quotes.txt
sed -n $(awk "END{ print $RANDOM%NR+1}" $quote)p $quote

A breakdown of the above
The quote variable is a path to the simple text file where my list of quotes are stored. Depending on your editor (I use Mac’s default, TextEdit), the quotes may wrap. That’s okay as long as you start each new quote on a separate line. Also leave a blank new line at the end of your file or else the PS1 of your prompt will appear on the same line directly after your quote.
This snippet awk "END{ print $RANDOM%NR+1}" $quote is actually using the Awk scripting language! We’re passing it options in the double quotes and an input file in the form of a variable (as defined on the line above it). Options:
The NR option returns the specified row number.
The END option counts the number of lines in the entire file.
Lastly, $RANDOM is a built-in bash variable that returns a random integer.
In this snippet, the total number of lines for the quotes file are calculated. We use this number as the denominator to the random number’s numerator and return the remainder. This is also called the modulo operation. We then increment by one in case the remainder happens to be zero—this ensures that a quote will always be returned.
Do you see how that whole code snippet is encapsulated in $()? Let’s call the number we just returned modulo for the rest of the breakdown.
Now what we’re left with is sed -n $(modulo)p $quote. sed isn’t bash—it’s actually a Unix utility called a stream editor! And like Awk, we can pass it options before passing the input file. By default, sed prints out all processed input so we use -n to suppress output and p to print specific lines. We already know from above that modulo is a random number that maps to the number of lines in your quote text file, therefore, you should see a random quote from your file print to the terminal!

I also have a pretty little bash prompt that shows me where I am in my directory, has custom colors, and will display git repos and branches as well (see picture). If you want to know more about this setup, DM me or comment in a thread. :grin:
