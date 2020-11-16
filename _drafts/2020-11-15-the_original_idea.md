---
layout: post
title: "The Original Idea"
date: 2020-11-15 23:28:00 -0400
featured-img: /img/post-images/model-map-v1.jpg
# categories: [Flatiron School]
tags: [Rails API, vanilla JavaScript, vanilla JS, JavaScript, JS, APIs]
excerpt: <p>Inspiration for great project ideas are often derived from your everyday activities. Think about the places you go, the services you use. What can be improved upon? What are they missing that might give them that little "extra something" to tip them over the edge of greatness? This post talks about an idea I had for one of my Flatiron School curriculum projects that was born from none other than the school's own learning platform.</p>
---

For my fourth portfolio project for what is beginning to feel like my tenure as a student at Flatiron School, I decided to create a tool specifically for my particular track of the Flatiron community (at least that's what my project started out as, but I'll save _that_ story for a different blog post.) You see, I'm enrolled in Flatiron School's online software engineering self-paced track and unlike the part-time and full-time cohorts, we aren't beholden to a set schedule where we have to keep up with the group and week to week. Instead, self-paced students have a 15-month period to complete their coursework and graduate, after which they can purchase time extensions. I feel extremely lucky to have began my coursework at Flatiron when I did because when I enrolled, I wasn't beholden to a time limit—which is the main reason I'm still here today, steadily working through the curriculum. I like to jokingly refer to myself as a "lifer." :D

Being a self-paced student has its pros and cons, but the main subject pertaining to this project is the support we receive from our instructors. When I began this project, we had a team of four dedicated self-paced instructors sharing the duties of holding office hours and conducting topic-based lectures, among other tasks. These sessions were held live over Zoom to enable student interaction and the topic-based lectures were almost always recorded for students to refer back to later or for those who couldn't attend the original study group session. I had some _**incredible**_ learning experiences in these study groups that I absolutely **never** could have had by watching a video recording alone. Actually, the very fact that Flatiron School provided these study groups was a huge influence in my decision to enroll in their bootcamp over another I was considering.

Since these sessions impact by learning experience so profoundly, when I had an idea to create a tool that would fulfill the requirements of the curriculum's fourth portfolio project and add value to Flatiron's self-paced student community, I got to work!

## The Original Idea

As I referred to in the first sentence of this post, right now I'm talking about my _**original**_ project idea, not what the finished product turned out to be ([sound familiar?](/2019/08/17/knowing_when_to_quit.md)). Keep that in mind as you read through the rest of this post.

I wanted to create a web app that would enable Flatiron students in the online self-paced to track make study group topic requests. They would then be able to see all topic requests and upvote the ones they like. This way the Flatiron instructors would be able to better tell which topics their students need more support with and plan their study groups accordingly.

## Models

I decided to create three models for this project: `User`, `Upvote`, and `Req`.

Below, you can see my model map which contains each model's attributes and associations.

>_**Confession Time:** Okay, truthfully my original app used the model name `Request` instead of `Req`, but when I got to the frontend part of my project I hit a major issue. I had errors popping up all over my console and had **no idea** where they were coming from! Then I got the idea to look up JavaScript's reserved words and—what do you know—`Request` is one of them! I changed it because I didn't want to use examples of bad code through my blog post. I promise the rest of this post is all factually accurate, exactly as it happened!_

![model map]

### Enum Attributes

There's one thing I want to highlight in the `User` model before we move on. Since this app is meant to be used by different types of users, I created a user enum attribute called `role`, which assigns the user one of the roles I predefined: `student`, `instructor`, or `super_admin`. See example below:

```ruby
# app/models/user.rb

class User < ApplicationRecord
  enum role: [:student, :instructor, :super_admin]

  # Alternatively you can use...
  # enum role: { student: 0, instructor: 1, super_admin: 2 }
  # This is a more explicit way of defining an enum attribute
end
```

>_**NOTE:**_ You **must** define the enum attribute's values in the model _**before**_ adding the enum attribute to the model in the database (aka running a migration). In other words, run your migrations for the model as normal _except_ leave out the enum attribute. Then in the model file, define the enum attribute's values as shown in the example above. Now run another migration adding the enum attribute to your model as an `integer` value. It's a good idea to set the default value to `0` as well so that each new instance of the model automatically takes on the first value in the enum attribute's list of values. Below is the migration code I used to add `role` as an enum attribute _**after**_ I created my `User` model and defined `role`'s attribute values.

```ruby
# app/db/migrate/date_add_role_to_users.rb

class AddRoleToUsers < ActiveRecord::Migration[6.0]
  def change
    add_column :users, :role, :integer, default: 0
  end
end
```

Using the `role` enum attribute allows the different types of users to interact with the app in different ways depending on which `role` they've been assigned. I won't go any further into enums, but in the future I plan to write a more details post about this handy type of attribute and its many built-in methods.

### Associations

As you can see in the [model map] above, `Upvote` acts as the join table between `Student` (an alias for `User`) and `Req`. This creates two types of student-owned requests:

1. When a `Student` creates a new `Req`

    ```ruby
      # app/models/user.rb

      class User < ApplicationRecord
        has_many :reqs, foreign_key: :student_id
      end
    ```

    ```ruby
      # app/models/req.rb

      class Req < ApplicationRecord
        belongs_to :student, class_name: "User"
      end
    ```

2. When a `Student` creates an `Upvote` on an existing `Req`

    ```ruby
      # app/models/user.rb

      class User < ApplicationRecord
        has_many :upvotes, foreign_key: :student_id
        has_many :upvoted_reqs, through: :upvotes, source: :reqs
      end
    ```

    ```ruby
      # app/models/upvote.rb

      class Upvote < ApplicationRecord
        belongs_to :student, class_name: "User"
        belongs_to :req
      end
    ```

    ```ruby
      # app/models/req.rb

      class Req < ApplicationRecord
        has_many :upvotes
        has_many :supporting_students, through: :upvotes, source: :student
      end
    ```

## The Look and Feel

Since this app was targeting a definite group of people—online self-paced software engineering students at Flation School—I decided to model it after Flatiron's Learn.co curriculum platform, specifically their login functionality, curriculum topics, and study group dashboard.

![Flatiron study group dashboard]

## User Flow

In my mind, the user flow would go something like this:

### Login

The student logs into the web app using their Flatiron School credentials or GitHub OAuth and is immediately directed to the study group dashboard. From there, they have the ability to navigate the app to view other students' requests or create their own request.

It's worth noting that creating any type of authentication system was by no means part of the project requirements, but the way my app was designed and modeled made it difficult to picture being used without it included.

### Navigating the App

The study group dashboard has a sidebar which contains a list of Flatiron's software engineering curriculum modules. This is also how the requests are ordered. Instead of being grouped and ordered by date like Flatiron's study group dashboard, they're grouped and ordered by module. The students can either scroll through the dashboard or select an option from the sidebar to jump to that particular module. From there, they can click the "Upvote" button on requests they like to boost its popularity and leave an optional comment. The upvote will then appear at the top of the dashboard along with any requests they themselves have previously created.

### Creating a New Request

Once the student has logged in, they'll see a "Create a New Request" button in the menu bar. Clicking this will open a modal form in which the student can input the request topic, select the appropriate module from a dropdown menu, and provide further information about the request in the description textarea field. Upon clicking "Submit", the modal clears, the study group dashboard scrolls to the module that was input in the form, and an alert triggers asking the student to check to make sure they're not submitting a duplicate request (the alternative being to upvote and leave a comment on the already existing request). The student then either opts to cancel their request, edit their request, or submit their request as is. Their request will then appear at the top of the dashboard along with any upvotes they've created on other students' requests.

### Logout

Also upon login, a "Logout" button will appear in the menu which the student can click to be logged out of the web app. Again, this is not part of the project requirements but if you have a login... you gotta have a logout too.

## In the End

Ultimately, I did not go forward with this particular plan. There were several reasons why, which as I said earlier could be a blog post on its own—and maybe it will some day. Instead, I created a very similar app with almost identical functions, but instead the resulting study sessions are meant to be more of a "crowdsourced" type of activity. Hopefully I'll be able to find or create a community that will really embrace this idea of self-teaching and I can see where it goes. Until then, I plan to redesign my finished project to be more easily expandable and find something _slightly_ more sophisticated than vanilla JavaScript to use when building the frontend.

[model map]: /img/post-images/model-map-v1.jpg "Model Map (v1)"
[Flatiron study group dashboard]: /img/post-images/fi-study-group-dashboard.jpg "Flatiron School's study group dashboard"
