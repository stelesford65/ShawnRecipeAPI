# Recipes API

## Part1 - Create the RESTful API app 
- Using the following command `rails new recipe-api --api -skip-active-storage` create a new rest API project

## Part2

Let's go ahead and create a model name it as `Recipe`. This model should be consist of the following `fields`.
 
|Field  | Data type | Usage
|--|--|--|
|  name | string | to store the recipe name |
|  ingredients | string | to store the list of ingredients |
|  directions | text | to store the recipe directions |
|  notes | string | to store extra information about the recipe | 
|  tag | string | list of tags that are associated with the recipe | 
