---
title: "Twitter Bot: Node.js and Twitter API v2.0"
description: "Building a Twitter Bot"
banner: "/images/sample-blog.jpeg"
tags: ["NextJS"]
date: 2023-01-01
---

### Twitter Bot: Node.js and Twitter API v2.0

Install node from [https://nodejs.org/en/download](https://nodejs.org/en/download)

CD to the application folder or create the project in Webstorm

To check if the nodejs has been installed tun `node -v` to get the version like 
> Create a new node app and install dependencies


`npm init -y` optional -y tag to say yes to all default options. 

It will create a package.json file in the folder
> Now add all the packages we will need for our bot.


```other
npm install twitter-api-v2
npm install dotenv
npm install cron
npm install express
```


Note if express command needs sudo elevation

To see installed packages in the current project as a dependency tree, use `npm list`

After installing the dependencies the root folder will have node_modules folder and package.json and package-lock.json
> Create an .env file in the root to store the API keys from twitter with the following


```other
NODE_ENV="development"
API_KEY="<your-API-key>"
API_SECRET="<your-API-secret>"
ACCESS_TOKEN="<your-access-token>"
ACCESS_SECRET="<your-access-secret>"
BEARER_TOKEN="<your-bearer-token>"

APP_ID="<your-app-id>"
```


The APP_ID is the first section of the ACCESS_TOKEN before the - 
> Now create a twitter client.


Create a new file called `twitterClient.js` and enter the following code.

```other
const { TwitterApi } = require("twitter-api-v2");

const client = new TwitterApi({
  appKey: process.env.API_KEY,
  appSecret: process.env.API_SECRET,
  accessToken: process.env.ACCESS_TOKEN,
  accessSecret: process.env.ACCESS_SECRET,
});

const bearer = new TwitterApi(process.env.BEARER_TOKEN);

const twitterClient = client.readWrite;
const twitterBearer = bearer.readOnly;

module.exports = { twitterClient, twitterBearer };
```


We will use the `twitterBearer` to read tweets, and the `twitterClient` to write to the platform e.g. likes, posts etc.
> Create index.js file and call the twitter API


Create an `index.js` file. This is where the app will run from. Add the following code

index.js

```other
require("dotenv").config({ path: __dirname + "/.env" });
const { twitterClient } = require("./twitterClient.js")

const tweet = async () => {
  try {
    await twitterClient.v2.tweet("Hello world!");
  } catch (e) {
    console.log(e)
  }
}

tweet();
```


Now in the terminal run `node index.js` 

The above code will import the `twitterClient` and tweet out "Hello world!". You can now go to Twitter and check whether the tweet was actually sent.
> Setup a cronjob (Optional)


Add the following constant at top of the index.js

```other
const CronJob = require("cron").CronJob;
```


And at the end of the index.js replace the tweet(); to add the following line.

```other
const cronTweet = new CronJob("30 * * * * *", async () => {
  tweet();
});

cronTweet.start();
```


The above cronjob formula runs the code every 30 seconds. To choose a preferable formula for intervals use [https://crontab.guru/](https://crontab.guru/)

Now after adding the cronjob codes the final index.js code should look like this. 

```other
require("dotenv").config({ path: __dirname + "/.env" });
const { twitterClient } = require("./twitterClient.js")
const CronJob = require("cron").CronJob;

const tweet = async () => {
  try {
    await twitterClient.v2.tweet("Hello world!");
  } catch (e) {
    console.log(e)
  }
}

const cronTweet = new CronJob("30 * * * * *", async () => {
  tweet();
});

cronTweet.start();
```


The code will fail, saying that you are not allowed to create a Tweet with duplicate content. So need to programmatically change the content to run a cronjob.
> Add express (Optional)


If you want to host this Twitter bot on a hosting platform like [heroku](https://heroku.com/) or [render](https://render.com), you will need to add express to your node.js app. This is because when hosting node.js applications, the server need a port to attach to.

To do that, simply add the following to your `index.js` file.

index.js

```other
const express = require('express')
const app = express()
const port = process.env.PORT || 4000;

app.listen(port, () => {
  console.log(`Listening on port ${port}`)
})
```


Your final `index.js file should look like this

index.js

```other
require("dotenv").config({ path: __dirname + "/.env" });
const express = require('express')
const app = express()
const port = process.env.PORT || 4000;
const { twitterClient } = require("./twitterClient.js")
const CronJob = require("cron").CronJob;

app.listen(port, () => {
  console.log(`Listening on port ${port}`)
})

const tweet = async () => {
  try {
    await twitterClient.v2.tweet("Hello world!");
  } catch (e) {
    console.log(e)
  }
}

const cronTweet = new CronJob("30 * * * * *", async () => {
  tweet();
});

cronTweet.start();
```


And that is it, your Twitter bot has been created. All that is left to do now is host your application on your favourite hosting platform.

Acknowledgement: This post has been followed from the post at [https://www.ryancarmody.dev/blog/creating-](https://www.ryancarmody.dev/blog/creating-a-twitter-bot-with-nodejs-api#step-5-create-an-indexjs-file-and-call-the-twitter-api)[a](https://www.ryancarmody.dev/blog/creating-a-twitter-bot-with-nodejs-api)[-twitter-bot-with-nodejs-api](https://www.ryancarmody.dev/blog/creating-a-twitter-bot-with-nodejs-api#step-5-create-an-indexjs-file-and-call-the-twitter-api)


---
A better way is to host the twitter bot using github actions for free. No hosting required. For this I followed the instructions on Matt Hughes youtube channel https://www.youtube.com/watch?v=wsA_kYRHoPY&t=10s
 and his github page https://github.com/zeepk/twitter-bot-template 
 
 
 Following youtube. tutorial https://www.youtube.com/watch?v=jl9OKxoqVcA to create a banner with recent follower pictures