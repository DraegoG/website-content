---
title: "Zeit Now Tutorial"
date: 2018-11-29T07:00:00+02:00
description: "Find out how to use the Now platform created by Zeit"
tags: services
---

One of the most simple ways to deploy a Node.js application is through the **Now** platform created by [Zeit](https://zeit.co).

> Now 2 was recently launched. This tutorials focuses on that. There are many differences from Now 1, [highlighted in this post](https://zeit.co/docs/v2/platform/upgrade-to-2-0).

Now makes the deployment and distribution step of an app very, very simple and fast. You can think of it as the "cloud", as you don't really know where your app will be deployed, but you know that you will have a URL where you can reach it.

You can use Now to deploy Node.js apps, Static Websites, and much more.

Now does not only support Node.js (also Go, PHP, Python and other languages), but in this tutorial I'll just consider this technology.

Now is free to start using, with generous free plan that includes 100GB of hosting, 1000 [serverless](/serverless/) functions invocations per day, 1000 builds per month, 100GB of bandwidth per month, and one [CDN](/cdn/) location. The [pricing page](https://zeit.co/pricing) helps get an idea of the costs if you need more.

## Installation

The best way is to install **Now Desktop**, which you can download from https://zeit.co/download. It's an [Electron](/electron/) application which also installs the **Now CLI**,  a tool we'll later use.

Through that, you can deploy applications using a simple drag and drop interface, really handy!

After starting, enter your email and Now will go on with the authentication, sending you a verification email.

![](Screen%20Shot%202018-11-08%20at%2019.14.42.png)

Once you are signed in, you can follow the quick tutorial:

![](Screen%20Shot%202018-11-08%20at%2019.16.39.png)

After you scroll through the few screens, the app is moved to the menu bar, and you when you click it, shows the activity feed:

![](Screen%20Shot%202018-11-08%20at%2019.18.11.png)

As you can see in this image, I installed Now a few months back with that email account, but didn't do much on it.

After signing in with the desktop application, the command line application called `now` is automatically signed in as well.

Jump into the [terminal](/macos-terminal/), and run `now`.

> Tip: if you don't need/want the desktop client, you can also just install the `now` CLI using the command `npm install -g now`. Then, you'll proceed to login using `now login`.

## Deploying an application on Now

For "application" we can just think about a simple HTML file, or a complex application with many build steps.

Whatever your app is, you can run

```bash
now
```

in a folder, and that folder will be uploaded to the cloud.

With just one caveat: the folder must contains a `now.json` file with (at least) this content:

```json
{
  "version": 2
}
```

to make sure the projects runs on Now 2.

Once you run the `now` program, the app is deployed to a random URL under the `now.sh` domain. In this case, it's `https://test-8h57iozp1.now.sh` and I just deployed an `index.html` file with `<p>test</p>` in its content:

![](Screen%20Shot%202018-11-08%20at%2020.02.14.png)

![](Screen%20Shot%202018-11-08%20at%2020.03.32.png)

After the deploy, the Now Desktop app lists this activity

![](Screen%20Shot%202018-11-09%20at%2009.54.03.png)

If you now change that index.html file content and run again `now`, you'll get a **different URL** for your app.

![](Screen%20Shot%202018-11-09%20at%2009.56.54.png)

This might be unexpected, right? Before it was `test-8h57iozp1.now.sh`, now it's `test-m2vcwrsc8.now.sh`. And **both URLs can be accessed**. Why?

![](Screen%20Shot%202018-11-09%20at%2009.59.59.png)

The expected behavior should be that the old URL is updated with the new content, but it's not.

Now has this concept of [immutability](https://zeit.co/docs/v2/deployments/concepts/immutability) that has many advantages, including the option of testing multiple releases at the same time, multiple developers working on different parts of an app, rollbacks, and more.

In production, or when you want to share your app, you need a fixed URL. It can't change every time you update it, right? To do this, you create an **alias**:

```bash
now alias test-m2vcwrsc8.now.sh test-flavio
```

![](Screen%20Shot%202018-11-09%20at%2011.05.37.png)

After you run this command, `test-flavio.now.sh` will point to that deploy.

Every time you want to update the deploy this alias points to, you run the command again. In this way you can freely test drive new releases, and when you are ok with making it the official one, you update the alias.

Same thing to rollback to a previous deploy, you just alias to the old deploy unique URL.

To remove a deployment, run `now rm <URL>`:

```bash
now rm test-m2vcwrsc8.now.sh
```

## Configure a lambda function

We can execute a Node.js application on demand when visiting a particular URL.

For example add a `test.js` file with this content:

```
module.exports = (req, res) => {
  res.end(`Hi!`)
}
```

In order to make it executable, we must add a build step to `now.json`:

```json
{
  "version": 2,
  "builds": [{ "src": "test.js", "use": "@now/node" }]
}
```

Head to <https://test-a0onzajf4.now.sh/test.js> to see the result ("Hi!")

![](Screen%20Shot%202018-11-09%20at%2011.32.59.png)

The curious thing is that now the `index.html` file does not load any more like before. This is because the default build step is overwritten, so we need to add one to fix this:

![](Screen%20Shot%202018-11-09%20at%2011.33.59.png)

Add the line `{ "src": "index.html", "use": "@now/static" }` to our build:

```json
{
  "version": 2,
  "builds": [
    {
      "src": "test.js",
      "use": "@now/node"
    },
    {
      "src": "index.html",
      "use": "@now/static"
    }
  ]
}
```

![](Screen%20Shot%202018-11-09%20at%2011.36.27.png)

## Where to go from here

There's lots more to find out about Now, but this tutorial will hopefully get you started in the right direction.

Some useful resources for you are

- [The Now Forum](https://spectrum.chat/zeit/now)
- [Now examples](https://github.com/zeit/now-examples)
- [Now boilerplates](https://github.com/zeit/awesome-zeit#boilerplates)
- [Now showcase](https://github.com/zeit/awesome-zeit#now-showcase)
- [Now helpers](https://github.com/zeit/awesome-zeit#helpers)