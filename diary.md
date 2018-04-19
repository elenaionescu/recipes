# The diary of developing this project

## Summary
### Implemented features:
recipe_list.feature
 - Scenario: No recipes available
 - Scenario: One recipe available
 - Scenario: Select a recipe
 - Scenario: Multiple recipes
 - Scenario: Multiple pages of recipes
 - Scenario: Navigating multiple pages of recipes

recipe.feature
 - Scenario: Recipe doesn't exists
 - Scenario: Recipe cooking time
 - Scenario: Recipe image
 - Scenario: Recipe ingredients

### Not Implemented:
star.feature
filter_recipes.feature

### Technology cover:
- React Router v4 (HTML5 History API)
- Create React App (Babel + Webpack + React + HotReloading)
- Express Server
- Bluebird - Promisifly fs module
- SASS
- ES 6 syntax
- ESlint
- Jest Test Runner, server side & client side
- JSDOM, Sinon stub & spy

### TODO:
- Cache fetched recipe and page
- data entry validation
- UX test - webdriver.io + selenium
- Image Optimisation (eg. compress, different resolution on different devices)
- CI flow - Travis CI


### Major Files done by me:
```
./RecipeListPageGenerator.js
./StatusGenerator.js
./preprocess.js
./server.js
./__test__/*.test.js
./recipes-client/src/Recipe.js
./recipes-client/src/Recipe.scss
./recipes-client/src/RecipeList.js
./recipes-client/src/RecipeList.scss
./recipes-client/src/App.js
./recipes-client/__test__/*.test.js
./data/recipes/*.json
./images/recipe/*
./README.md
```

Choose create-react-app for frontend, since we dont need to config tones of things to get the app work.
Choose Jest as the test runner on both side, since react provided and do not want to have different test runner on server.

According the difficulty on yestraday estimation, my flow will as follow:
1. setup env for development
2. setup data set of recipe
3. backend implementation
 - recipe api by name, return json
 - recipe list feature, create /page/1.json , /page/2.json etc for pagination
    - pre process with npm rather than create on start.
    - order by cookingTime
 - filter feature, provide in memory data for frontend filtering
  - by name, create a Set of recipe_name
  - by cookingTime, create an Array in asc order, use lower_bound to find the cursor of less than provided minute.
  - by ingredient, create a key-value dict.
   - ingredient_name as key, value is an array of recipe_name
 - star recipe by login user.
  - using passport Oauth sign in.
4. frontend implementation
 - start implementation on recipe component
 - start implementation on recipe list component
 - start implementation on filter componet
 - start implementation on star componet
5. webdriver.io + selenium for end to end UX test.
6. deploy flow? TODO


Nodejs + Express for the backend,
frontend could use React, no Redux should use since no sharing state (no global state as I seen)
react-router as a single page application

Qs:
1. where is the data, should it be a CSV file, e.g. recipe.csv
 - No, we just json format for better indication of nested properties.

2. seach result of the data, in memory search ? what if data are too large. (file base search?) anything need to index?

3. how to scale, what if number of recipe > 10K, how to manage?
 - probably need a database.

4. should provide CMS for inputting data?
 - didn't have the time to implement.

5. should the filter done on frontend ? Since the data is not huge, we could let all data preload in clientside,
otherwise should be a backend query to minimize the network traffic. we could use solr as well.

Assumption:
1. no Database needed, recipe < 150
2. in memory search is enough


prepare recipe as JSON format, each recipe has its own file, unique name.

```JSON:
{
    "cookingTimeInMinutes": 60,
    "ImageUrl": "",
    "ingredients": [
        {
            "name": "",
            "quantity": "1 tsp"
        }
    ]
}
```
how to represent the user?
```
{
    "name" : "John",
    "fav": [1,2,3,4],
    "oauth_token": ""
}
```
how to authenticate a user?

oauth? using google, facebook, Linkin? [npm passport]

how to create a new user? oauth

how to store user? filebase "./user/${unique_oauth_id}.json"

if user existed, create session and record any new fav recipe

difficulty:  myfav feature > filter > recipe list page with pagination > recipe detail page

url parttern:
 - /recipe/${recipe-filename} for recipt detail page
 - / for RLP

how to test?

for User experience in browser, we could use selinum + webdriver.io

and mocha test case for javascript code

optimization:
Server Side Rendering on initial load

