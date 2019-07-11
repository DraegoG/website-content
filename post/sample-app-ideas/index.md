---
title: "A list of sample Web App Ideas"
date: 2018-02-19T08:04:59+02:00
updated: 2018-05-14T08:04:59+02:00
description: "Every time I start a tutorial I find myself in a limbo wondering which app should I build. A to-do app? Not again!"
tags: js
---

If you're reading this post you are looking for an idea, a simple app that you can use in your tutorial or in your example project to test a new framework or API, but you can't find anything that really resonates with you.

It needs to be simple enough but at the same time complex enough to be worth doing.

> "I don't want to build another to-do app", I hear you thinking.

I wrote this post to help myself, and I hope this will help you as well.

Some of the ideas are self-contained (not involving the use of an external API), some make use of famous public APIs where you can easily grab pre-built data.

Some require a server part, some do not, which might also depend on your implementation.

But I try to keep those ideas:

- good to build a tutorial
- good to experiment with web technologies
- not something that will take a week to figure out
- not "startup ideas"
- I do not target mobile apps but web apps
- easy to explain
- easy to build (less than 24 hours if prepared)
- easy to extend with new features

So, enough talk, here's the list!

<!-- TOC -->

- [Simple apps](#simple-apps)
  - [A weight tracker app](#a-weight-tracker-app)
  - [A calculator app](#a-calculator-app)
  - [A book database](#a-book-database)
  - [A recipes app](#a-recipes-app)
  - [A bill tracker](#a-bill-tracker)
  - [An expenses tracker](#an-expenses-tracker)
  - [A chat application](#a-chat-application)
  - [A notes app](#a-notes-app)
  - [A personal diary app](#a-personal-diary-app)
  - [A pomodoro app](#a-pomodoro-app)
  - [A meme generator](#a-meme-generator)
  - [Tic-tac-toe game](#tic-tac-toe-game)
  - [The game of life](#the-game-of-life)
  - [A blog engine](#a-blog-engine)
  - [A QA engine](#a-qa-engine)
  - [A forum engine](#a-forum-engine)
  - [An embeddable live chat](#an-embeddable-live-chat)
- [API-powered apps](#api-powered-apps)
  - [A Hacker News client](#a-hacker-news-client)
  - [A Reddit client](#a-reddit-client)
  - [An Instagram client](#an-instagram-client)
  - [A GitHub API client](#a-github-api-client)
  - [An Unsplash API client](#an-unsplash-api-client)
- [Data for your sample apps](#data-for-your-sample-apps)
  - [Public APIs you can use in example projects](#public-apis-you-can-use-in-example-projects)
  - [Image placeholders for your sample projects](#image-placeholders-for-your-sample-projects)
  - [Image generators](#image-generators)
  - [Sample text generator for your sample projects](#sample-text-generator-for-your-sample-projects)
  - [Other fake data](#other-fake-data)
- [Wrapping up](#wrapping-up)

<!-- /TOC -->

## Simple apps

### A weight tracker app

- It accepts a set of manual entries of weight measurements taken at different dates
- It can plot a graph
- It can allow to track multiple entities, for example more than one person weight
- Store them somewhere

### A calculator app

A standard calculator: numbers, +, -, \*, /, and the result

[See video tutorial](https://www.youtube.com/watch?v=Drnp29SJY8w)

### A book database

- Enter the books you own
- Enter the books you'd like to buy
- Store the book info, images

### A recipes app

- Enter a name, a description with the steps
- Have pictures
- Have some ranking for difficulty and quality
- Add the time needed
- Have different steps with a picture for each
- Store them somewhere

[See video tutorial](https://www.youtube.com/watch?v=6tZ4c-Bxstg)

### A bill tracker

- Log bills, amounts and date
- List bills
- Have a few graphs (this year / last year)
- Store them somewhere

### An expenses tracker

- Log expenses, tag them (or have categories)
- List expenses
- Have a few graphs (last month / last year)
- Store them somewhere

### A chat application

- Some sort of stripped-down Slack
- People enter without authentication and are assigned a name, stored for when they come back
- Store the history
- Add notifications

### A notes app

- Add a new note
- List all your notes in the sidebar
- Store them somewhere

### A personal diary app

- Add entries with a date and text
- Entries have a date
- Show more recent first
- Attach pictures
- Store them somewhere

### A pomodoro app

- Enter a time
- Start timer
- Alert when the time is over

[See video tutorial](https://www.youtube.com/watch?v=lgj3nfzV0xM)

### A meme generator

- Have 10 popular meme images
- Let the user add the text
- Result is image + text
- Store the history

### Tic-tac-toe game

We all know what a tic-tac-toe game is 🙂

[See video tutorial](https://www.youtube.com/watch?v=Ia69O1ZNGEg)

### The game of life

A great project involving math and graphics.

[See video tutorial](https://www.youtube.com/watch?v=5Ajcjs3OmjA)

### A blog engine

- Allow to login and add posts
- Visitors can add comments
- Store the data somewhere

### A QA engine

- Allow to login
- Allow to add questions
- Allow to answer to questions
- Allow original user to choose the best question
- Store the data somewhere

### A forum engine

- Allow to login
- Allow to add posts
- Allow to comment on posts
- Store the data somewhere

### An embeddable live chat

Think Intercom or Olark.

- Have a "backend" where you respond
- Embed on a web page
- Let people write to you privately

---

## API-powered apps

### A Hacker News client

- List the popular posts
- Show a post comments
- Show a user profile
- Search HN

Check [HNPWA](https://hnpwa.com/) and [Awesome Hacker News](https://github.com/cheeaun/awesome-hacker-news) for inspiration

### A Reddit client

- List the popular posts
- List the comments of a post
- Show a user profile

### An Instagram client

- Enter an hashtag and get the latest posts
- Enter a username and get the latest posts
- Allow to store one or more hashtags/usernames and get all the latest posts from those

### A GitHub API client

- List the popular repositories from today / week / month
- List the latest commits in a repository
- Show a person or organization public repositories ranked by stars

### An Unsplash API client

- Search images by topic
- Let the user enter a term, show relevant images

Start at [Unsplash API](https://unsplash.com/developers)

---

## Data for your sample apps

Sometimes you start doing some simple app, but you're bored at finding data you can use. You don't have to, you can use real data, or random data.

### Public APIs you can use in example projects

Maybe you have an idea for a perfectly nice CRUD app, or something that works with an API, but you don't want to create the API in the first place.

I recommend to check out [Airtable](/airtable/), which provides a great API for developers, very easy to use, like a database.

There are amazing public APIs you can use:

- [The Cat API](https://thecatapi.com/docs.html)
- [The Dog API](https://dog.ceo/dog-api/)
- [The Chuck Norris API](https://api.chucknorris.io/)
- [Fuck Off As A Service API](https://www.foaas.com/)
- [Quotes API](https://favqs.com/api)
- [Quotes API](http://forismatic.com/en/api/)
- [The Spotify API](https://beta.developer.spotify.com/documentation/web-api/)
- [The New York Times API](https://developer.nytimes.com/)
- [The Wikipedia API](https://www.mediawiki.org/wiki/API:Main_page)
- [The Wikidata API](https://www.wikidata.org/w/api.php?action=help)
- [The Medium API](https://github.com/Medium/medium-api-docs)
- [Design Quotes API](https://quotesondesign.com/api-v4-0/)
- [The GoodReads API](https://www.goodreads.com/api)
- [The Dribbble API](http://developer.dribbble.com/v2/)
- [The 500px API](https://github.com/500px/api-documentation)
- [The Unsplash API](https://unsplash.com/developers)
- [The Giphy API - GIFs!](https://developers.giphy.com/docs/)
- [The Pixabay API](https://pixabay.com/sk/service/about/api/)
- [Exchange rates](https://exchangeratesapi.io/)
- [Site screenshots API](https://apileap.com/)
- [The Oxford Dictionary API](https://developer.oxforddictionaries.com/)
- [Website Technologies API](https://github.com/letsvalidate/api)
- [The Mapbox API](https://www.mapbox.com/developers/)
- [Music Lyrics API by Genius](https://docs.genius.com/)
- [Site meta tags API](http://bettermeta.io/)
- [The EventBrite API](https://www.eventbrite.com/developer/v3/)
- [Open source projects changelogs](https://changelogs.md/)
- [The GitHub REST API](https://developer.github.com/v3/)
- [The GitHub GraphQL API](https://developer.github.com/v4/)
- [QR codes API](http://goqr.me/api/)
- [The StackExchange API](https://api.stackexchange.com/)
- [Words and synonyms](https://www.wordsapi.com/)
- [The Nasa API](https://api.nasa.gov/)
- [The SpaceX API](https://github.com/r-spacex/SpaceX-API)
- [The Hacker News API](https://github.com/HackerNews/API)
- [The Instagram API](https://instagram.com/developer/)
- [The Reddit API](https://www.reddit.com/dev/api)
- [The Slack API](https://api.slack.com/)
- [The Twitter API](https://developer.twitter.com/en/docs)
- [The YouTube API](https://developers.google.com/youtube/)

### Image placeholders for your sample projects

- [Placeholder.com](https://placeholder.com/)
- [Placekitten](https://placekitten.com/)

### Image generators

Avatars:

- [RoboHash](https://robohash.org/)
- [Adorable Avatars](http://avatars.adorable.io/)
- [DiceBear Avatars](https://avatars.dicebear.com/) (pixel art)

### Sample text generator for your sample projects

Lorem Ipsum is boring. Spice it up:

- [Cat Ipsum](http://www.catipsum.com/index.php)
- [Bacon Ipsum](https://baconipsum.com/)
- [Cupcake Ipsum](http://www.cupcakeipsum.com/)
- [Hipster Ipsum](https://hipsum.co/)
- [Office Ipsum](http://officeipsum.com/)
- [Samuel L. Ipsum](http://slipsum.com/)
- [Zombie Ipsum](http://www.zombieipsum.com/)
- [Doctor Ipsum](http://doctoripsum.com/)
- [SF Ipsum](http://www.sfipsum.com/)

If you insist on using Lorem Ipsum, [Loripsum](https://loripsum.net/) is a good generator.

### Other fake data

[FakeJSON](https://fakejson.com/) has tons of fake data generation capabilities.

[JSONPlaceholder](http://jsonplaceholder.typicode.com/) has fake posts, comments, photos, todos, users, albums ready for REST consumption.

Need fake name/user data generation? Check [UI Names](https://github.com/thm/uinames) and [RandomUser](https://randomuser.me/)

## Wrapping up

I hope this list is comprehensive enough to suit your needs!

Have fun!
