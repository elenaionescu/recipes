# The Challenge

There is a request for a new food / recipe application that will help users become better at cooking.
Unfortunately the product manager has dumped a bunch of specifications on you and done a runner!

Your task is to develop an application that fulfils _some_ or _all_ of the specification provided.

## What are we looking for?

The aim of the task is to give you the opportunity to show **your** skills in web development. The specification is deliberately open for that reason. If you aren't strong in front-end development or you haven't done much server-side development, don't worry... **Play to your strengths!**

We are also very interested in _non-coding_ aspects and how you approach problems. Please supply any notes you make, such as showing your working, questions you might want to ask and assumptions you may have made. We also **strongly** recommend you use comments in any code you supply to communicate your reasoning as you work.

The languages that will be accepted are:-

• JavaScript
• Node.js
• React.js

The `features` folder contains the behavioural specifications of the application to be built. Start by reading through these feature files, they should give you a sense of what is required.


## Setup

`yarn install && cd recipes-client && yarn install`

## Run

`yarn run preprocess && yarn start`

## Test

`yarn test` for testing the serverside.
for clientside testing, we will use `yarn test` under `/recipes-client`

**REMARK** After test will remove build files. You will have to RUN again.

## Deploy

First you have to build (server + client) code:
`yarn build` in the parent directory.

Then you can start your server in parent directory:
`NODE_ENV=production yarn run server`

After that, you need to setup reverse proxy to serve on 80 port from 3001.


## Input Recipe

Put your recipe under folder /data/recipes , each recipe must have a **Unique** recipe name as filename, the format must follow the standard:
```javascript
{
    "cookingTimeInMinutes": 60,
    "imageUrl": "/images/recipe/${your_png_filename}",
    "ingredients": [
        {
            "name": "Sugar",
            "quantity": "1 tsp"
        },
        {
            "name":  "chicken",
            "quantity": 2
        }
    ]
}
```

## Input Recipe Image

Put image file under `./images/recipe/`

## Project Structure

This project structure is base on the idea from [here](https://www.fullstackreact.com/articles/using-create-react-app-with-a-server/)

In behind, we use create-react-app(webpack + babel + react) for frontend, express for backend.

[**Jest**](https://facebook.github.io/jest/) as the Test runner.

For details, please read **diary.md**


