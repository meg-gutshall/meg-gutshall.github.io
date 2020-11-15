---
layout: post
title: "JWT Auth Rails"
date: 2020-11-14 23:28:00 -0400
featured-img: /img/post-images/cash.jpg
# categories: [Flatiron School]
tags: [Rails API, JWT, JSON Web Tokens, authorization]
excerpt: <p>Excerpt</p>
---

## The Project

_First paragraph is a brief overview of my JS project and what models it uses, which brings me to users and authentication._

I knew I was going to be implementing a User model in my app, so on the advice of one of my codepanions (s/o to Sushi!), I followed [Flatiron School's Jwt Auth Rails lesson][JWT Auth Rails] step-by-step and got it working relatively easily. Well... okay, I did run into a teensy snag along the way, but a quick stop-in at JavaScript Project Office Hours with the infallible Alice Balbuena helped me sort that out right quick and I was on my way to building out the rest of my project!

## The Point

Now, I know the aforementioned lesson is a walkthrough of using the JWT authentication implementation, so why write a blog post about coding a step-by-step walkthrough? **Perspective, yall!!** There are so many different combinations of code that can be written to achieve the same goal, how could there not be multiple ways to teach that code as well?

Plus, there are quite a few hyperlinks in Flatiron's lesson that go into further detail on auth implementation, JWTs, storing tokens, etc. Having a naturally curious mind, I tend to follow these links down rabbit holes hoping to quench my insatiable thirst for knowledge and end up coming back with TL;DR's to share with my codepanions!

Another point on perspective, teaching something to others helps me learn it even better. Therefore, I am including a Code Talk study session I held as a walkthrough of this particular lesson.

_*Insert video here._

## The Pitfall (and Other Possibilities)

On to the snag... I followed everything the way I thought it was supposed to be, but for some reason, I just couldn't get a fetch request to go through. (Note: I was testing my code using Postman.) It turns out there was a discrepancy between the strong params in my Users controller and my fetch body. Add more details and the issue, why it was a problem, and how it was solved.

_Add any other obvious possible pitfalls in this section._

## Conclusion

_Sum up all that was covered in this blog post and important parts of the lesson itself that were highlighted._

## Sources

- [JWT Auth Rails]
- [Postman]

[JWT Auth Rails]: https://learn.co/lessons/jwt-auth-rails "JWT Auth Rails – Learn.co"
[Postman]: https://www.postman.com/ "Postman"
