---
layout: post
title: "Hacktoberfest"
date: 2020-11-27 17:33:00 -0500
featured-img: /img/post-images/
# categories: [Flatiron School]
tags: []
excerpt: <p>Excerpt</p>
---

Video recording: [https://youtu.be/b-DMt3q7ieI](https://youtu.be/b-DMt3q7ieI)
Video chat: [http://bit.ly/code-talk-hacktoberfest-2019-chat](http://bit.ly/code-talk-hacktoberfest-2019-chat)
Shortlink for these notes: [http://bit.ly/code-talk-hacktoberfest](http://bit.ly/code-talk-hacktoberfest)

<!-- TODO -->
- [ ] Update for 2020
- [ ] Make sure all resources are current/relevant
- [ ] Split post in half
- [ ] Insert images
- [ ] Be sure to s/o Paula

## What Is Hacktoberfest?

Hacktoberfest is a month-long celebration of open source software hosted by DigitalOcean, and this year, DEV! It's held annually in October (this year being the 6th) and open to the global community. It was started to encourage contributions to the open source ecosystem by both beginners and veterans alike.

## What Is Open Source?

Open source software is classified as being freely available to everyone without restrictions. This means it is free of cost, the source code is available for use and/or modification by users, and it can be freely redistributed. The Open Source Initiative (OSI) gives a more detailed definition of open source.

### Great, that's Nice. You Mentioned Swag...

Yep! For the first 50,000 people to make four valid pull requests during Hacktoberfest, they will be sent a limited edition t-shirt in the mail along with STICKERS!

### Sweet! How Do I Get in on Hacktoberfest?

It's crazy super simple! Go to the Hacktoberfest home page at [https://hacktoberfest.digitalocean.com/](https://hacktoberfest.digitalocean.com/) and click on the purple 'Start Hacking' button either in the middle left or at the top right corner... unless you have your window shrunk up all small, then it's smack dab in the middle cuz DigitalOcean designed a kick-ass responsive website—that's what I'm talkin' BOUT!

Whew! Okay, I'm calm now.

You'll be redirected to a page where you sign in through GitHub. What's that authentication strategy called again? &#10033;cough&#10033; _My Flatiron School codepanions at the end of the Rails section should be shouting it out right now…_ &#10033;cough&#10033; OmniAuth!!

Once you sign in through GitHub, you'll be able to visit your Hacktoberfest profile page ([https://hacktoberfest.digitalocean.com/profile](https://hacktoberfest.digitalocean.com/profile)) to check on your status. It's definitely possible that almost all of my Flatiron codepanions will already have the four commits required to win the t-shirt. How is that possible you ask? Well, the good folks at DigitalOcean declared a month-long celebration and meant it! No matter when you actually register for Hacktoberfest, as long as it's during the month of October, all pull requests created between October 1st and October 31st will count toward your total. And how do they decide what "counts" anyway? It's pretty straightforward.

## Tha Rulez

1. You gotta register. Check. ✔
2. Now, make four pull requests (PRs) in any GitHub-hosted repository or project between Oct 1–31. There are stipulations to this rule so listen up:
    1. If a maintainer of a repository/project you contributed to reports your PR as invalid or behavior not in line with their code of conduct, you will be ineligible to participate. This may happen if you submit an unhelpful or spammy contribution. Quality > quantity.
    2. Draft PRs will not be counted toward Hacktoberfest.
    3. [Introducing Draft Pull Requests](https://github.blog/2019-02-14-introducing-draft-pull-requests/) <sup>[5]</sup>
    4. This year all GitHub PRs count toward Hacktoberfest, not just the ones with issues labeled "Hacktoberfest".
    5. PRs do not have to be merged and accepted to count toward Hacktoberfest.
    6. **Note:** Your PRs are in a pending state until you submit the required four. Once you reach that goal, your one-week review begins in which the repository/project maintainers can identify any invalid PRs. If any are marked invalid, it will show in your Hacktoberfest profile and you will remain in a pending state until you reach four PRs again in which the review period will restart. I repeat, quality > quantity!

So why do you have to make your contributions through GitHub?

**TL;DR:** GitHub is fucking awesome.

### How GitHub Facilitates Open Source

As you well know, GitHub is a major estate for open-source software. One reason is the ease with which GitHub incorporates transparency throughout the build process by clearly tracking changes through commits. Another reason is GitHub allows users to collaborate on open-source projects in real time by implementing a tool that flags conflicts between different versions of the project so code isn't accidentally overwritten. These GitHub features, plus many more, allow users to quickly and easily collaborate on open-source software in a more dynamic and forgiving manner, because if any issues arise, there are plenty of ways to return to the last "stable" point in the project.

## How Do I Do the Thing? (aka GitHub Pull Requests 101)

Okay, so we're registered and we may or may not already have our four pull requests through Flatiron School's Learn.co curriculum, but it's Hacktoberfest—let's keep coding!

### Forking

Once you find a project that you'd like to work on (see below for **plenty** of resources on where to look), you'll fork the repository. You do this by clicking the 'Fork' button in the upper right-hand corner of the repository page, located underneath your user icon. You'll briefly see a loading screen displaying an image of a book being scanned with a fork stuck in it's cover. Next, you'll be redirected to a repository page but instead, you will now own the project instead of the original maintainer. You just made your own copy of the repo.

**Note:** Each GitHub repository has a URL that looks something like `https://github.com/username/repository-name`. Notice that the original project's URL was `https://github.com/repo-owner-username/repository-name` but after you forked it, it's `now https://github.com/your-username/repository-name`. In fact, you can see at the top of your repository page, `your-username/repository-name` with "forked from `repo-owner-username/repository-name`" listed in small text immediately underneath.

### Cloning

To make a copy of your forked repository on your computer, open up a new terminal window and navigate (`cd`) into the directory where you want to store the project. Next, go back to the browser and click the green 'Clone or download' button on your repository page, copying the SSH URL. Return to the terminal, type `git clone`, and then paste in the copied URL and press enter to clone down your forked repo.

At this point you'll also want to add your upstream. An upstream is...

<!-- TODO: Add this info --> What is an upstream? How to add it. -->

>Hey Meg, FWIW, here are blogs I found “beginner-ish readable” about upstream / downstream. They’re in order of how easy I found them to understand!  Not confident yet about the process, so I’m not gonna attempt to write this section! - Paula
>[https://outofmymemory.wordpress.com/2013/09/18/what-is-the-difference-between-origin-and-upstream-in-github/](https://outofmymemory.wordpress.com/2013/09/18/what-is-the-difference-between-origin-and-upstream-in-github/)
>[https://nearsoft.com/blog/how-to-synchronize-your-github-fork/](https://nearsoft.com/blog/how-to-synchronize-your-github-fork/)
>[https://www.atlassian.com/git/tutorials/git-forks-and-upstreams](https://www.atlassian.com/git/tutorials/git-forks-and-upstreams)

### Branching

The default branch of a repo is called the main branch.<sup>[6]</sup> If you're contributing to someone else's project, it is good practice to create a new branch in which to make your alterations. Give it a short but descriptive name as to what you'll be doing in the branch, using hyphens instead of spaces. To do this, in the terminal `cd` into your repo directory and use the `git checkout -b` command followed by the name. This creates a new branch in the local copy of your repository and switches into that branch. To switch back to main (or any other branch), just type `git checkout` followed by the branch's name.

<!-- TODO: 6: Say something about the switch from master to main. -->

### Commit, Commit, Commit...

After you've made changes to the code (modified existing code, added a file, deleted code or a file), it's time to track them. We do this in two steps:

  1. Stage our changes. Type `git add .` to prepare all the changes you've made so far to be saved. **Note**: There's a difference between `git add .` and `git add -A`.<sup>[4]</sup>
  2. Track, or save, our changes by committing them using the `git commit` command. Commits have two important jobs: they keep track of how our project looks each step of the build process (a process called version control) and maintain a written log of the changes made throughout the build and why they were made.

It is important to commit often in order to capture your project at all different stages of the build. If you choose to work on Hacktoberfest labeled issues, you may not make as many commits as usual due to the natural specificity of issues. However, just as you apply Separation of Concerns and the Single Responsibility Principle in crafting your code, you should do the same in deciding when to commit.

### ...Message

If the changes we want to save are very simple (say, fixing a typo or changing a color), you can type `git commit -m` followed by a short commit message in quotation marks. If they need more description, run the `git commit` command and this will trigger your default text editor<sup>[7]</sup> to open with a prompt document in which to type your commit message.

There will be some commented-out lines at the top with directions and info on the staged changes. Underneath this, write a summary of your commit message (around 50 characters long) and then begin a new line. GitHub has tools to easily show file changes. What you need to include in the body of your commit message is why you made the changes. You can do so using bullet points or full sentences, just as long as it's understandable. Once you are satisfied, save and close the commit message file.

<!-- TODO: Move the note below to an aside or something of that nature. -->

<sup>[7]</sup>**Note:** You can configure your default text editor right from your terminal. The following are configuration options using some of the most popular editors right now:

- VS Code: `git config --global core.editor "code --wait"`
- Atom: `git config --global core.editor "atom --wait"`
- Sublime (Mac): `git config --global core.editor "subl -n -w"`
- Sublime (Win, 32-bit install): `git config --global core.editor "'c:/program files (x86)/sublime text 3/sublimetext.exe' -w"`
- Sublime (Win, 64-bit install): `git config --global core.editor "'c:/program files/sublime text 3/sublimetext.exe' -w"`

### Push It

You've saved your changes locally, now you have to update your remote repository—the copy that is hosted on GitHub. To do this, type the command `git push -u origin new-branch` in the terminal.

<!-- TODO: Break down parts of this command. -->

### Pull It

<!-- TODO: How to create a pull request. -->

### Bop It!

Haha! Just kidding!

### Rebase

<!-- TODO: Figure this monster out… Or just make a different blog for it. Undecided. -->

>Meg -- here’s a good site about rebase, but I’m not touching it in any attempt to write a how-to here!   :-o   Paula
[https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase)

## The Importance of Open Source Software -- For Everyone

"Contributing to open-source projects helps ensure that they are as good as they can be and representative of the broad base of technology end-users. When end-users contribute to open-source projects through code or documentation, their diverse perspectives provide added value to the project, the project’s end-users, and the larger developer community."<sup>[1]</sup>

It may all seem overwhelming and grandiose to think of it in these broad terms, especially if you're feeling a bit of Imposter's Syndrome lately, but every programmer can add something of value to the open source community. If you're a beginner, you may look at an app with 10,000 lines of code in it and then call me crazy; but if you did, you would be overlooking a very important part of the source code: the documentation.

Many developers forget what it's like to feel completely lost when you're just beginning to learn a new language, framework, whatever. As a new programmer, you have an advantage in that you're still learning how to read and interpret documentation—and you're starting to notice that some documentation is much easier to read than others. Start looking at the documentation for software that you already use regularly. If you find documentation that could be more clear, fork the repo and clone it down! Reword it or add in clarifying pieces that you would have liked to see when you were struggling to get a handle on the software it describes. Then commit, push it back up to your fork, and submit your pull request. Be sure to give a brief explanation in your PR as to why you felt like the documentation needed adjustment, and remember—the maintainer can't sense your tone, so keep it friendly!

## A List of Open Source Projects

Here are some resources that are great for beginners to start with:<sup>[2]</sup>

- Up For Grabs: [https://up-for-grabs.net/](https://up-for-grabs.net/)
- GitHub Issue Finder: [https://gityouanissue.com/3](https://gityouanissue.com/3)
- Issuehub: [http://issuehub.io/](http://issuehub.io/)
- First Timers Only: [https://www.firsttimersonly.com/](https://www.firsttimersonly.com/)
- Your First PR: [http://yourfirstpr.github.io/](http://yourfirstpr.github.io/)
- Awesome for Beginners: [https://github.com/mungell/awesome-for-beginners](https://github.com/mungell/awesome-for-beginners)

Here are some resources for people who are a bit more comfortable working with open-source projects:<sup>[2]</sup>

- Hacktoberfest projects: [https://hacktoberfest.digitalocean.com/#projects](https://hacktoberfest.digitalocean.com/#projects)
- Open issues on GitHub labeled "Hacktoberfest": [https://github.com/search?l=&o=desc&q=label%3Ahacktoberfest+state%3Aopen&s=updated&type=Issues](https://github.com/search?l=&o=desc&q=label%3Ahacktoberfest+state%3Aopen&s=updated&type=Issues)
- Pull Request Roulette: [http://www.pullrequestroulette.com/](http://www.pullrequestroulette.com/)
- Code Triage: [https://www.codetriage.com/](https://www.codetriage.com/)
- 24 Pull Requests: [https://24pullrequests.com/](https://24pullrequests.com/) (You bet your ass I'm going to bring this back for the holidays!)
- Contrib: [https://gauger.io/contrib/#/language/javascript](https://gauger.io/contrib/#/language/javascript)

The following projects/organizations I have either worked on/with or they were recommended to me by other trusted devs:

- [Ruby for Good](https://rubyforgood.org/): A volunteer-driven nonprofit that develops specialized technology and software solutions for non-profit organizations to bolster their critical missions
  - [CASA](https://github.com/rubyforgood/casa): Volunteer management system for nonprofit CASA, which serves foster youth in counties across America (Ruby, HTML, JavaScript, Shell, SCSS, Dockerfile)
  - [Terrastories](https://github.com/Terrastories/terrastories): A geostorytelling application built to enable local communities to locate and map their own oral storytelling traditions about places of significant meaning or value to them (Ruby, JavaScript, HTML, SCSS, Dickerfile, Shell, Gherkin)
  - [Mutual Aid](https://github.com/rubyforgood/mutual-aid): A mutual aid management platform for groups who build, support, and strengthen community resilience (Ruby, HTML, Vue, JavaScript, SCSS, Shell, Dockerfile)
  - [Circulate](https://github.com/rubyforgood/circulate): An operating system for lending libraries (Ruby, HTML, SCSS, JavaScript, Shell, Dockerfile)
  - [Diaper](https://github.com/rubyforgood/diaper): Diaperbase is an inventory system for diaper banks, to aid them in tracking their inventory and providing statistics about their inventory flows. (Ruby, SCSS, HTML, JavaScript)
  - [Partner](https://github.com/rubyforgood/partner): Partner and companion app for the Diaper app (SCSS, Ruby, HTML)
  - [Voices of Consent](https://github.com/rubyforgood/voices-of-consent): Open source tracking and inventory management application for the nonprofit. (Ruby, HTML, JavaScript, CSS)
  - [Abalone](https://github.com/rubyforgood/abalone): A data tracking and analytics app for abalone conservation efforts live at [http://abalone.blrice.net/](http://abalone.blrice.net/) (Ruby, HTML, JavaScript, SCSS, Makefile, Dockerfile)
- [Code for America](https://www.codeforamerica.org/): On a mission to make government work for the people who need it most in the digital age
  - [Intake](https://github.com/codeforamerica/intake): A Django project behind the Clear My Record website (Python, HTML, SCSS, Less, JavaScript, Gherkin)
  - [Honeycrisp Design System (CFA Styleguide Gem)](https://github.com/codeforamerica/honeycrisp-gem): A Rails gem with base styles and Javascript for Code for America products (Ruby, SCSS, HTML, JavaScript, Shell)
  - [Ohana Web Search](https://github.com/codeforamerica/ohana-web-search): A mobile-friendly website for finding human and social services in your community (CSS, Ruby, JavaScript, HTML)
  - [Ohana API](https://github.com/codeforamerica/ohana-api): The open source API directory of community social services (Ruby, Haml, PLpgSQL, HTML, SCSS, JavaScript)
  - [Code for America Hurricane Response](https://github.com/hurricane-response): Multi-brigade effort building off of the work done for Harvey, Irma, Florence & Michael
    - [Response Hub](https://github.com/hurricane-response/response-hub): Main hub/landing page at [https://www.hurricane-response.org/](https://www.hurricane-response.org/) (HTML, CSS, Ruby, JavaScript)
    - [Response Theme](https://github.com/hurricane-response/response-theme): Jekyll theme scaffold for deploying CFA disaster response/shelter tracking map (HTML, CSS, Ruby, JavaScript)
    - [Florence API](https://github.com/hurricane-response/florence-api): Fork of [https://github.com/sketch-city/harvey-api](https://github.com/sketch-city/harvey-api) for Hurricane Florence (Ruby, HTML, JavaScript, CSS)
    - [SMS Location Bot](https://github.com/hurricane-response/sms-location-bot): I’m a bot! You send me a location via SMS, and I reply with the nearest location I know of for the thing I know how to locate (JavaScript)
- [Open Referral](https://github.com/openreferral/): We develop data standards and open platforms that make it easy to share and find information about community resources (HTML, JavaScript, Ruby, CSS, Java)
- [HTTPX](https://github.com/encode/httpx): A next generation HTTP client for Python (Python, Shell)
- [GraphQL Engine](https://github.com/hasura/graphql-engine): Blazing fast, instant realtime GraphQL APIs on Postgres with fine grained access control, also trigger webhooks on database events (Haskell, JavaScript, TypeScript, Go, Python, CSS)
- [Strawberry](https://github.com/strawberry-graphql/strawberry): A new GraphQL library for Python (Python)

## Four PRs! I Am an Open Source Master!

Yes, you totally are!! I know it, you know it, and DigitalOcean knows it. In fact, once your Hacktoberfest PRs all attain that lovely pink 'Eligible' checkbox status, you should be hearing from them via email to submit your t-shirt order! If it's been a few weeks (give 'em time, 50,000 is a lot of orders to fill) and you're still waiting to place your t-shirt order, give them a quick "just checking in" email at [hacktoberfest@digitalocean.com](mailto:hacktoberfest@digitalocean.com). You can use this email for most questions that aren't already answered on their site's [FAQ](https://hacktoberfest.digitalocean.com/faq) page.

You did it. Congratulations! But don't lose steam now—keep those contributions going throughout the year! Every time you wear your new Hacktoberfest t-shirt, ask yourself what kind of developer do you want to be: an annual Hacktoberfest participant with the sole objective of winning a free t-shirt or an open source contributor who collaboratively fixes issues while giving back to the online community?

## Other Goodies & Resources

### More Swag! Can't Get Enough!

New to DigitalOcean? Receive USD $50 in infrastructure credit at [https://do.co/hacktoberfest50](https://do.co/hacktoberfest50).
Hacktoberfest 2019 Swag List: [https://hacktoberfestswaglist.com/](https://hacktoberfestswaglist.com/)

### More Resources

Open Source Guides: [https://opensource.guide/how-to-contribute/](https://opensource.guide/how-to-contribute/)
DEV Open Source Articles: [https://dev.to/t/opensource](https://dev.to/t/opensource)
An Introduction to Open Source (Tutorial by DigitalOcean): [https://www.digitalocean.com/community/tutorial_series/an-introduction-to-open-source](https://www.digitalocean.com/community/tutorial_series/an-introduction-to-open-source)
Documentation as an Open Source Practice: [https://blog.digitalocean.com/documentation-as-an-open-source-practice/](https://blog.digitalocean.com/documentation-as-an-open-source-practice/)
Git Cheat Sheets: [https://github.github.com/training-kit/](https://github.github.com/training-kit/)
Understanding the GitHub Flow: [https://guides.github.com/introduction/flow/](https://guides.github.com/introduction/flow/)
GitHub Patchwork: [http://patchwork.github.io/](http://patchwork.github.io/)
Flatiron: Mac OSX Manual Environment Setup: [https://help.learn.co/en/articles/900121-mac-osx-manual-environment-set-up](https://help.learn.co/en/articles/900121-mac-osx-manual-environment-set-up)
Flatiron: Setting Up Linux Virtual Box: [https://help.learn.co/en/articles/1489324-setting-up-linux-virtual-box](https://help.learn.co/en/articles/1489324-setting-up-linux-virtual-box)

## Sources

1. [https://www.digitalocean.com/community/tutorials/how-to-contribute-to-open-source-getting-started-with-git](https://www.digitalocean.com/community/tutorials/how-to-contribute-to-open-source-getting-started-with-git)
2. [https://hacktoberfest.digitalocean.com/details](https://hacktoberfest.digitalocean.com/details)
3. I met the dev who built this at a freeCodeCamp Philly meetup. _Which means by proxy I'm almost famous._ Here's his GitHub: [https://github.com/rheupler](https://github.com/rheupler). Check it out—it's pretty cool!
4. [https://gist.github.com/dsernst/ee240ae8cac2c98e7d5d](https://gist.github.com/dsernst/ee240ae8cac2c98e7d5d)
5. Thank you Anthony for passing along this resource and being a super active participant in the Code Talk!
