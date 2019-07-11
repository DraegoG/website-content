---
title: "Glitch, a great Platform for Developers"
date: 2018-05-03T07:06:15+02:00
description: "Glitch is a pretty amazing platform to learn and experiment with code. This post introduces you to Glitch and makes you go from zero to hero"
tags: services
---

[Glitch](https://glitch.com/) is a great platform to learn how to code.

I use Glitch on many of my tutorials, I think it's a **great tool** to **showcase** concepts, and also **allow people to use your projects** and build upon them.

Here is an example project I made on Glitch with [React](/react/) and [React Router](/react-router/): <https://glitch.com/edit/#!/flaviocopes-react-router-v4>

<!-- Copy and Paste Me -->
<div class="glitch-embed-wrap" style="height: 553px; width: 100%;">
  <iframe src="https://glitch.com/embed/#!/embed/flaviocopes-react-router-v4-2?path=app/app.jsx&previewFirst=true&sidebarCollapsed=true" alt="flaviocopes-react-router-v4-2 on glitch" style="height: 100%; width: 100%; border: 0;"></iframe>
</div>

With Glitch you can easily create **demos** and **prototypes** of applications written in JavaScript, from simple web pages to advanced frameworks such as React or [Vue](/vue-introduction/), and server-side Node.js apps.

It is built on top of **Node**, and you have the ability to install any [npm](/npm/) package you want, run [webpack](/webpack/) and much more.

It's brought to you by the people that made some hugely successful products, including Trello and Stack Overflow, so it has a lot of credibility bonuses for that.

## Why do I think Glitch is great?

Glitch "clicked" for me in how it presents itself in a **funny** interface, but **not dumbed down**.

You have access to **logs**, the **console**, and lots of internal stuff.

Also, the concept of remixing so prominent in the interface makes me much more likely to create lots of projects there, as I never have to start from a clean slate.

You can start diving into the code **without losing time** setting up an environment, version control, and focus on the idea, with an automatic **HTTPS** URL and a [**CDN**](/cdn/) for the media assets.

Also, there's no lock-in at all, it's just Node.js (or if you don't use server-side JavaScript, it's just HTML, JS and CSS)

## Is it free?

**Yes**, it's free, and in the future they might add even more features on top for a paid plan, but they state that the current Glitch will always be free as it is now.

There are reasonable limits like

- You have 128MB of space, excluding npm packages, plus 512MB for media assets
- You can serve up to 4000 requests per hour
- Apps are stopped if not accessed for 5 minutes and they do not receive any HTTP request, and long running apps are stopped after 12 hours. As soon as an HTTP request comes in, they start again

## An overview of Glitch

This is the Glitch homepage, it shows a few projects that they decided to showcase because they are cool, and some starter projects:

![The homepage as guest](home-guest.png)

Creating an account is free and easy, just press "Sign in" and choose between Facebook and GitHub as your "entry points" (I recommend GitHub):

![Sign in to Glitch](signin-button.png)

You are redirected to GitHub to authorize:

![Authorize Glitch on GitHub](signin-github.png)

Once logged in, the home page changes to also show your projects:

![The home page once logged in](home-logged.png)

Clicking **Your Projects** sends you to your profile page, which has your name in the URL. Mine is <https://glitch.com/@flaviocopes>.

![The Glitch profile](profile.png)

You can **pin** projects, to find them more easily when you'll have lots of them.

## The concept of remixing

When you first start, of course you will have no projects of your own.

Glitch makes it super easy to start, and you never start from a blank project. **You always _remix_ another project**.

You can remix a project you like, maybe one you found on Twitter or featured in the Glitch homepage, or you can start from a project that's a boilerplate to start something:

- [A simple web page](https://glitch.com/~hello-webpage)
- [Node.js Express app](https://glitch.com/~hello-express)
- [A Node.js console](https://glitch.com/~node-console)
- [A Create-React-App app](https://glitch.com/~create-react-app-sample)
- [A Nuxt starter app](https://glitch.com/~nuxt-starter)

There are many other starter glitches in these collections:

- [Hello World Glitches](https://glitch.com/hello-worlds)
- [Building Blocks](https://glitch.com/building-blocks)

If you're learning to code right now, the [Learn to Code glitch Collection](https://glitch.com/learn-to-code) is very nice.

I have created a few starter apps that I constantly use for my demos and tests, and they are:

- [Simple HTML + CSS + JS glitch](https://glitch.com/~flaviocopes-html-basic)
- [React + webpack starter glitch](https://glitch.com/~flaviocopes-starter-react)

Glitch makes it very easy to create your own building blocks, and by pinning them in your profile, you can have them always on the top, easy to find.

## Remix a glitch

Once you have a glitch you want to build upon, you just click it, and a window shows up:

![Remix glitch modal](single-glitch-modal.png)

There are 3 buttons:

- **Preview** a glitch is code that does something. This shows the result of the glitch.
- **Edit Project** shows the source of the project, and you can start editing it
- **Remix This** clones the glitch to a new one

Every time you remix a glitch, a new project is created, with a random name.

Here is a glitch right after creating it by remixing another one:

![A remixed glitch](remixed-glitch.png)

Glitch gave it the name `guttural-noodle`. Clicking the name you can change it:

![Rename a glitch](change-name.png)

You can also change the description.

From here you can also create a new glitch from zero, remix the current glitch, or go to another one.

## GitHub import/export

There is an easy import/export from/to GitHub, which is very convenient:

![GitHub Import export](glitch-github.png)

## Keep your project private

Clicking the lock makes the glitch private:

![Keep project private](private-glitch.png)

## Create a new project

Clicking "New Project" shows 3 options:

- node-app
- node-sqlite
- webpage

![Create a new project on Glitch](new-project.png)

This is a shortcut to going out to find those starter apps, and remix them. Under the hoods, clicking one of those options remixes an existing glitch.

On any glitch, clicking "Show" will open a new tab where the app is run:

![The app running](app-running.png)

## App URL

Notice the URL, it's:

`https://flavio-my-nice-project.glitch.me`

That reflects the app name.

The editing URL is a bit different:

`https://glitch.com/edit/#!/flavio-my-nice-project`

The preview runs on a subdomain of `glitch.me`, while editing is done on `glitch.com`.

Noticed the fishes on the right of the page? It's a little JavaScript that Glitch recommend to add to the page, to let other people remix the project or see the source:

![The fish on preview](glitch-preview-fishes.png)

## Running the app

Any time you make a change to the source, the app is rebuilt, and the live view is refreshed.

This is so convenient, real time applying changes gives an immediate feedback that's a great help when developing.

## Secrets

You don't want any API key or password that might be used in the code to be seen by everyone. Any of those secret strings must be put in the special `.env` file, which has a key next to it.

If you invite collaborators, they will be able to see the content, as they are part of the project.

But anyone remixing it, or people invited by you to help, will not see the file content.

## Managing files

Adding a new file to a project is easy.

You can **drag and drop files and folders from your local computer**, or click the "**New File**" button above the files list.

It's also intuitive how to rename, copy or delete files:

![Manage the glitch](copy-delete-rename.png)

## One-click license and code of conduct

Having a license in the code is one of the things that's overlooked in sample projects, but determines what others can do, or can't do, with your project. Without a license, a project is not open source, and all rights are reserved, so the code cannot be redistributed, and other people cannot do anything with it (note: this is my understanding and IANAL - I Am Not A Lawyer).

Glitch makes it _super easy_ to add a license, in the **New File** panel:

![Add a license](add-license.png)

![View the license](view-license.png)

You can easily change it as well:

![Change the license](edit-license.png)

The code of conduct is another very important piece for any project and community. It makes contributors feel welcomed and protected in their participation to the community.

The **Add Code of Conduct** button adds a sample code of conduct for open source projects you can start from.

## Adding an npm package

Click the `package.json` file, and if you don't have one yet, create an empty one.

Click the **Add Package** button that now appears on top, and you can add new package.

![Add an npm package](add-package.png)

Also, if you have a package that needs to be updated, Glitch will show the number of packages that need an update, and you can update them to the latest release with a simple click:

![Update dependencies](update-packages.png)

## Use a custom version of Node.js

You can set the Node.js version to [any of these](https://nodeversions.glitch.me/) in your `package.json`. Using `.x` will use the latest release of a major version, which is the most useful thing, like this:

```json
{
  //...
  "engines": {
    "node": "8.x"
  }
}
```

## Storage

Glitch has a persistent file system. Files are kept on disk even if your app is stopped, or you don't use if for a long time.

This allows you to store data on disk, using local databases or file-based storage (flat-file).

If you put your data in the `.data` folder, this special name indicates the content will not be copied to a new project with the glitch is remixed.

## Embedding a glitch in a page

Key to using Glitch to create tutorials is the ability to embed the code and the presentation view, in a page.

Click **Share** and **Embed Project** to open the Embed Project view. From there you can choose to only embed the code, the app, or customize the height of the widget - and get its HTML code to put on your site:

![Embed glitch](embed-glitch.png)

## Collaborating on a glitch

From the Share panel, the **Invite Collaborators to edit** link lets you invite anyone to edit the glitch in real time with you.

You can see their changes as they make it. It's pretty cool!

## Asking for help

Linked to this collaboration feature, there's a great one: you can ask help from anyone in the world, just by selecting some text in the page, and click the raised hand icon:

![Ask for help on a line](ask-help-1.png)

This opens a panel where you can add a language tag, and a brief description of what you need:

![Describe your problem](ask-help-2.png)

Once done, your request will be shown in the Glitch homepage for anyone to pick up.

When a person jumps in to help, they see the line you highlighted, and I found that comments made a good way to communicate like a chat:

![Help out someone](helping.png)

## See the logs

Click **Logs** to have access to all the logs of the app:

![The project logs](logs.png)

## Access the console

From the Logs panel, there is a **Console** button. Click it to open the interactive console in a separate tab in the browser:

![The project console](console.png)

## The debugger

Clicking the **Debugger** button in the Logs panel, an instance of the Chrome DevTools opens in another tab with a link to the debugger URL.

![The debugger](debugger.png)

## The changes history

A great feature is the ability to check all your changes in the project history.

It's a lot like how Git works - in fact, under the hoods it's Git powering this really easy to use interface, which opens clicking the ⏪ button:

![The history of changes](history.png)

## How is Glitch different than Codepen or JSFiddle?

One big difference that separates Glitch from other tools is the ability to run server-side code.

Codepen and JSFiddle can only run frontend code, while a Glitch can even be used as a lightweight server for your apps - keeping the usage limits in mind.

For example I have set up an Express.js server that is triggered by a Webhook at specific times during the day to perform some duties. I don't need to worry about it running on another server, I just wrote it on Glitch and run directly from there.

## That's it!

I hope you like my small tutorial on using Glitch, and I hope I explained most of the killer features of it.

## More questions?

I suggest to just try it, and see if it clicks for you too.

The [Glitch FAQ](https://glitch.com/faq) is a great place to start.

Have fun!
