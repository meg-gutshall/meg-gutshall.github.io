---
layout: post
title: "What's Up With That!?: ActiveRecord Enums"
date: 2020-05-26 15:29:00 -0500
featured-img: /img/post-images/activerecord-enums/teacher.jpg
# categories: [Flatiron School, What's Up With That?]
tags: [enum, enums, Rails, Ruby, ActiveRecord]
excerpt: <p>The word "enums" sounded intimidating to me for a while, like something everyone knew about and I somehow missed that day in class. But after digging into the docs (Read the docs!), I've found they're simple to set up and have handy methods that come built right in!</p>
---

Oh, the illusive ActiveRecord enums... for a while it was just a word I heard occasionally, usually thrown out as a solution when I'd rubber duck with a friend about how to programmatically represent a certain type of object: "You could always use an enum." I'd shake my head agreeably and silently hope I wouldn't be probed about it any further.

Well the time to create my fourth portfolio project came around and I started brainstorming, landing on my [Flatiron Study group dashboard][Everyday Inspiration] idea. As I stubbed out my models and attributes, I realized that I'd need a few different user types. After [the disaster that resulted from my first foray into using two different user types with Devise][Knowing When to Quit], I knew I wanted to be more careful with this project, so I decided to look into ActiveRecord enums and see how they could help in this situation—and I'm glad I did! Not only are they easy to use, but they also come with built-in methods and queries that make them incredibly powerful!

## How to Create an Enum Attribute

Since my app was created to serve different types of users, I decided to add an enum attribute called `role` to my `User` model. The `role` attribute will assign the user a role from a list of defined values: `student`, `instructor`, or `admin`.

### Steps

1. First, we must define the enum attribute's values in the model ***before*** adding the enum attribute to the model in the database (aka running a migration). In other words, we run our migration for the model as usual *except* we omit the enum attribute.

    ```ruby
    # app/models/user.rb
    class User < ApplicationRecord
      # Other user model code goes here...
    end
    ```

2. Next we define the enum attribute's values in the model file.

    ```ruby
    # app/models/user.rb
    class User < ApplicationRecord
      enum role: [:student, :instructor, :admin]

      # Other user model code goes here...
    end
    ```

3. *Now* we can run the migration which adds the enum attribute to our model as an `integer` along with its values.

    ```bash
    rails g migration AddRoleToUsers role
    ```

    ```ruby
    # app/db/migrate/date_add_role_to_users.rb
    class AddRoleToUsers < ActiveRecord::Migration
      def change
        add_column :users, :role, :integer, default: 0
      end
    end
    ```

<aside class="note">
  <p>
    <span class="teal ital">Note:</span>
    <span class="ital">It's good practice to set the default value to <code class="highlighter-rouge language-plaintext">0</code> here. This way we know that each new instance of the model will automatically take on the first value in the enum attribute's list of values—in this case, the <code class="highlighter-rouge language-plaintext">student</code> role.</span>
  </p>
</aside>

And that's it! Our `role` enum attribute is set up and ready to go! Pretty easy, right? Almost magical? I hate to burst your bubble but it's not magic—nothing in Rails is!—it's the enum attribute's values mapping to integers in the database. Also Santa isn't real.

### Enums: Getting Our Hands Dirty

If you don't care much to learn the nitty-gritty, feel free to skip ahead to the next section where I go over what you can actually **do** with ActiveRecord enums. If you're like me and wouldn't have been satisfied with the surface-level explanation above, we'll get *just* a hair deeper in (don't worry, I have some solid resources linked at the end of this post).

Per the step-by-step instructions above, we had to define our ActiveRecord enum attribute and its values in our model ***before*** creating and running the migration file. What's up with that? Does it really matter that much when you add your attribute onto your model? The answer is yes!

The example shown above is the "Rails magic" shorthand version of declaring an enum attribute. The explicit way to declare this attribute and its values would be:

```ruby
# app/models/user.rb
class User < ApplicationRecord
  enum role: { student: 0, instructor: 1, admin: 2 }

  # Other user model code goes here...
end
```

As you can see, each value in the enum attribute hash is explicitly mapped to the database via the migration file that declared `role` as an integer.

Although the first declaration which uses an array to implicitly map the values to the database is admittedly prettier, the database integers depend solely on the order the values appeared in the array at the time we run the migration. That means the `[:student, :instructor, :admin]` order must be maintained. Luckily, there's a class method available with which we can call the pluralized form of our enum attribute name that will return the mapping in a `HashWithIndifferentAccess` ([see docs][HashWithIndifferentAccess]).

```ruby
User.roles[:student]      # => 0
User.roles["instructor"]  # => 1
User.roles[:admin]        # => 2

# HashWithIndifferentAccess allows [:key] and ["key"] to be considered equal.
```

Hopefully we all have a better understanding of how enums are constructed. In creating our `role` enum attribute, we've just enabled our users to interact with the app in different ways depending on which `role` they've been assigned. Now, here are the methods behind the magic!

## Available Methods & Queries

### Basic Methods

Continuing with our example, much like other attributes, we can hard code the value of the `role` enum attribute—just so long as it's one of the values declared in our `User` model.

```ruby
user.role = nil
user.role.nil?  # => true
user.role       # => nil

user.role = 0
user.role = "student"
# The two lines above are equivalent
user.role  # => "student"
```

### Boolean & Dangerous Methods

Additionally, Rails creates boolean (`?`) and dangerous (`!`) methods for each value, or in this case, accessor and update methods. Boolean methods (also called predicates or query methods) end with a question mark and return either `true` or `false`. Dangerous methods (also called mutator or bang methods) end with the bang operator (`!`) and return the modified object.

```ruby
user.update! role: 1
user.instructor!
# The two lines above are equivalent
user.instructor? # => true
user.role        # => "instructor"

user.admin?  # => false
user.admin!  # This line is changing the value of user's role attribute from instructor to admin
user.admin?  # => true
```

### Scopes

Scopes based on the allowed values of the enum attribute are provided as well.

```ruby
User.roles  # => { "student" => 0, "instructor" => 1, "admin" => 2 }

User.student      # Returns all student users
User.not_student  # Returns all instructor and admin users

User.instructor       # Returns all instructor users
User.not_instructor   # Returns all student and admin users

User.admin      # Returns all admin users
User.not_admin  # Returns all student and instructor users
```

### ActiveRecord Queries

Remember, you can always query the `User` class directly using ActiveRecord.

```ruby
# All queries return an ActiveRecord::Relation object
User.where(role: :student)    # Returns all student users
User.where(role: :instructor) # Returns all instructor users
User.where(role: :admin)      # Returns all admin users

# Returns all instructor and admin users
User.where.not(role: :student)
User.where(role: [:instructor, :admin])

# Returns all student and admin users
User.where.not(role: :instructor)
User.where(role: [:student, :admin])

# Returns all student and instructor users
User.where.not(role: :admin)
User.where(role: [:student, :instructor])
```

## Still Curious?

I know I've only scratched the surface with this post. In fact, there are a few other methods in [the docs][Enum] that I didn't even mention here! Also if you want to read another rather succinct intro post on the same topic, check out [Creating Easy, Readable Attributes With ActiveRecord Enums].

There are several blog posts out there that guide you through the steps on how to save the enum attribute's values to the database as *strings* rather than integers. Here's two of them: [Enums with Rails & ActiveRecord: an improved way] & [Ruby on Rails - How to Create Perfect Enum in 5 Steps]. These will get you more comfortable with SQL for sure! You could also use the [str_enum gem] and it'll take care of all of that for you, no SQL required!

If you enjoyed this intro to ActiveRecord enums, let me know [@meg_gutshall](https://twitter.com/meg_gutshall)! Or better yet, share it with a friend!

<!-- All Hyperlinks -->
<!-- Backlinks -->
[Everyday Inspiration]: https://meghangutshall.com/2020/11/16/everyday_inspiration/
[Knowing When to Quit]: https://meghangutshall.com/2019/08/17/knowing_when_to_quit
<!-- Docs -->
[HashWithIndifferentAccess]: https://api.rubyonrails.org/classes/ActiveSupport/HashWithIndifferentAccess.html
[Enum]: https://api.rubyonrails.org/classes/ActiveRecord/Enum.html
<!-- Resources -->
[Creating Easy, Readable Attributes With ActiveRecord Enums]: https://www.justinweiss.com/articles/creating-easy-readable-attributes-with-activerecord-enums/
[Enums with Rails & ActiveRecord: an improved way]: https://sipsandbits.com/2018/04/30/using-database-native-enums-with-rails/
[Ruby on Rails - How to Create Perfect Enum in 5 Steps]: https://naturaily.com/blog/ruby-on-rails-enum
[str_enum gem]: https://github.com/ankane/str_enum
