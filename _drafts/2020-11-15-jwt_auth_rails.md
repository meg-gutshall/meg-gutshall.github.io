---
layout: post
title: "JWT Auth Rails"
date: 2020-11-15 23:28:00 -0400
featured-img: /img/post-images/model-map-v1.jpg
# categories: [Flatiron School]
tags: [Rails API, JWT, JSON Web Tokens, authorization]
excerpt: <p>Excerpt</p>
---

This post pertains to my fourth project at Flatiron School, specifically my v1 plan which [you can read about in this blog post](2020/11/15/the_original_idea/).

<!-- Give a **tiny** intro about my app. **TINY!!!** -->

## The Point

I knew I was going to be implementing a User model in my app, so on the advice of one of my codepanions (s/o to Sushi!), I followed [Flatiron School's Jwt Auth Rails lesson][JWT Auth Rails] step-by-step and got it working relatively easily. Well... okay, I did run into a teensy snag along the way, but a quick stop-in at JavaScript Project Office Hours with the infallible Alice Balbuena helped me sort that out right quick and I was on my way to building out the rest of my project!

Now, I know the aforementioned lesson is a walkthrough of using the JWT authentication implementation, so why write a blog post about coding a step-by-step walkthrough? **Perspective, yall!!** There are so many different combinations of code that can be written to achieve the same goal, how could there not be multiple ways to teach that code as well?

Plus, there are quite a few hyperlinks in Flatiron's lesson that go into further detail on auth implementation, JWTs, storing tokens, etc. Having a naturally curious mind, I tend to follow these links down rabbit holes hoping to quench my insatiable thirst for knowledge and end up coming back with TL;DRs to share with my codepanions!

Another point on perspective: Teaching something to others helps me learn it even better, so I'll also share with you a few things I learned along the way during my build.

## The Pitfall (and Other Possibilities)

On to the snag... I followed everything the way I thought it was supposed to be, but for some reason, I just couldn't get a fetch request to go through. (Note: I was testing my code using [Postman].) It turns out there was a discrepancy between the strong params in my Users controller and my fetch body. _Add more details and the issue, why it was a problem, and how it was solved. Look at [this commit](https://github.com/meg-gutshall/code-talk-requests-frontend/commit/0c74f3b5ff2a520aa4b6d02995554e2f15fb5cb1) to see the fix. Basically I needed to nest my login form credentials inside a user object before passing it to the stringify method in order to fulfill the "require" part of the strong params._

_Add any other obvious possible pitfalls in this section—like the fact that there's no logout function._

## JWT's Extra Features

See [this commit](https://github.com/meg-gutshall/code-talk-requests-backend/commit/cb785cb6dd356da239da6304b6220ba5b1ce976f) for more details on what to write about.

## Implementing a Logout Function

For some odd reason the lesson does not include instructions on how to logout and they're _really_ difficult to find online.

- Clear the browser's local storage
- Send a DELETE fetch to the backend to clear the session

## Conclusion

_Sum up all that was covered in this blog post and important parts of the lesson itself that were highlighted._

## Sources

- [JWT Auth Rails]
- [Postman]

[JWT Auth Rails]: https://learn.co/lessons/jwt-auth-rails "JWT Auth Rails – Learn.co"
[Postman]: https://www.postman.com/ "Postman"

### Notes

- Consider using pictures/diagrams from the Jwt Auth Rails lesson
- Look at the lesson's "External Resources" section for more info
- Insert code blocks where necessary
