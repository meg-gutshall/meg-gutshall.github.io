---
layout: post
title: "JWT Auth Rails"
date: 2020-11-14 23:28:00 -0400
featured-img: /img/post-images/cash.jpg
# categories: [Flatiron School]
tags: [Rails API, JWT, JSON Web Tokens, authorization]
excerpt: <p>Excerpt</p>
---

For my fourth portfolio project for what is beginning to feel like my tenure as a student at Flatiron School, I decided to create a tool specifically for my particular track of the Flatiron community (at least that's what my project started out as, but I'll save _that_ story for a different blog post.) You see, I'm enrolled in Flatiron School's online software engineering self-paced track and unlike the part-time and full-time cohorts, we aren't beholden to a set schedule where we have to keep up with the group and week to week. Instead, self-paced students have a 15-month period to complete their coursework and graduate, after which they can purchase time extensions. I feel extremely lucky to have began my coursework at Flatiron when I did because when I enrolled, I wasn't beholden to a time limit—which is the main reason I'm still here today, steadily working through the curriculum. I like to jokingly refer to myself as a "lifer." :D

Being a self-paced student has its pros and cons, but the main subject pertaining to this project is the support we receive from our instructors. When I began this project, we had a team of four dedicated self-paced instructors sharing the duties of holding office hours and conducting topic-based lectures, among other tasks. These sessions were held live over Zoom to enable student interaction and the topic-based lectures were almost always recorded for students to refer back to later or for those who couldn't attend the original study group session. I had some _**incredible**_ learning experiences in these study groups that I absolutely **never** could have had by watching a video recording alone. Actually, the very fact that Flatiron School provided these study groups was a huge influence in my decision to enroll in their bootcamp over another I was considering.

Since these sessions impact by learning experience so profoundly, when I had an idea to create a tool that would fulfill the requirements of the curriculum's fourth portfolio project and add value to Flatiron's self-paced student community, I got to work!

## The Project

_First paragraph is a brief overview of my JS project and what models it uses, which brings me to users and authentication._

I knew I was going to be implementing a User model in my app, so on the advice of one of my codepanions (s/o to Sushi!), I followed [Flatiron School's Jwt Auth Rails lesson][JWT Auth Rails] step-by-step and got it working relatively easily. Well... okay, I did run into a teensy snag along the way, but a quick stop-in at JavaScript Project Office Hours with the infallible Alice Balbuena helped me sort that out right quick and I was on my way to building out the rest of my project!

## The Point

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
