# Recipes API Part 2

Now we'll build further upon our `recipes-api` from [yesterday's homework](https://git.generalassemb.ly/SEIR-629/W08-D02-HW). 

You'll need to either repeat the steps from that assignment in this directory (recommended!) or copy and paste your project directory from that repo into this one.

>If you cloned this repo into the same parent directory as yesterday's repo, then from within the *original* project directory (`/recipes-api`) you can type `cp -r . ../../W08-D02-HW-P2/recipes-api` to copy yesterday's Rails project into this repo.

## Part1 - create a model

Let's create another model, this one named `Recipe`. This model should consist of the following fields:

|Field  | Data type | Usage
|--|--|--|
|  name | string | to store the recipe name |
|  ingredients | string | to store the list of ingredients |
|  directions | text | to store the recipe directions |
|  notes | string | to store extra information about the recipe |
|  tags | string | list of tags that are associated with the recipe |

Great! So far we haven't created the Recipe table yet, and this is the ideal time to think about the relationship between `Recipe` and `Category` tables. In a real-world application, there could be many recipes that belong to a given category. We can create this `reference` inside our `Recipe` table.
>Have you created a reference in a migration in Rails before? How? You'll probably do something similar here.

You can generate the model and migration from the command line with `rails g model Recipe`, then update the migration to build your `recipes` table as described above. Once you're finished defining all the fields and the reference, don't forget to migrate the table.

If you finished the task correctly, the final ER diagram should look like this.

![Model categories](final-erd.png)

## Part2 - add model associations  

Now we just need to update our two model files to reflect the associations we need for our API:

File path ```app/models/category.rb```

Change from
```ruby
class Category < ApplicationRecord
end
```

to

```ruby
class Category < ApplicationRecord
  # model association
  has_many :recipes, dependent: :destroy

  # validations
  validates_presence_of :title, :created_by
end
```

File path ```app/models/recipe.rb```

Change from

```ruby
class Recipe < ApplicationRecord
end
```

to

```ruby
class Recipe < ApplicationRecord
  # model association
  belongs_to :category

  # validation
  validates_presence_of :name
end
```

>Can you explain what we just did? If not, find a classmate and *try* to explain -- then have them *try* to explain the same to you.

## Part3 - create a controller  

Create a controller for `recipes` using the following command: `rails generate controller recipes`.

The RESTful API must consist of the endpoints (CRUD).

|Prefix| Verb|URI Pattern| Controller#Action |
|--|--|--|--|
|recipes|GET| /recipes(.:format)| recipes#index|
||POST|/recipes(.:format)|recipes#create|
|recipe|GET|/recipes/:id(.:format)|recipes#show|
||PATCH|/recipes/:id(.:format)|recipes#update|
||PUT|/recipes/:id(.:format)|recipes#update|
||DELETE|/recipes/:id(.:format)|recipes#destroy|

## Part4 - create routes

In `config/routes.rb` make any necessary changes to enable each controller at its designated endpoint. Run `rails routes` to ensure that the results match your expectations.

## Part4 - Test your RESTful API using POSTMAN

Test each route to make sure it functions according to spec.

Every route works? Congratulations!

## How to submit homework

### Setup

- Step 1. Fork the repository
- Step 2. Clone your fork
- Step 3. Incorporate the first part of this project by following the directions at the top of this repo.

### Submitting work

- Step 1. Push to your fork
- Step 2. Submit a pull request
- Step 2.1. Add a title (First name, Last Name) and comment

In the comment section, you must add the following:

```text
* Comfort Level [0 to 5]
* Completeness [0 to 5]
* What was a win?
* What was a challenge?
* Any other comments
```
