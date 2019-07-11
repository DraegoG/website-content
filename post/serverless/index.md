---
title: "What is Serverless?"
date: 2018-12-29T07:00:00+02:00
description: "What is serverless and why should you care?"
---

Serverless is a term that identifies a particular way to run programs, that does not involve managing your own server.

You create a **function**, place it somewhere in a cloud server, and all you have is a URL to call.

When you call that URL, the function is executed.

Someone else manages the server, the scaling, the security. There's no need to worry about kernel updates or moving to the next LTS release of your Linux distribution.

Serverless is very convenient from the pricing model too. Traditionally you might rent a VPS (Virtual Private Server) monthly, and pay for the monthly price regardless of your actual usage.

If you have a spike of users because someone shared your website in a popular place, the server might not be able to serve all requests unless you upgrade to a bigger server.

With serverless, **you pay for requests** rather than paying for the server. If no one is using your service, you pay nothing. If 100.000 people jump on your site all together, your functions scale because the company that manages the functions for you has all the elements in place for handling the traffic and automatically put more resources into your functions. You pay for the resource used rather than for some resource you might use in the future.

When done right, it also proves to be very liberating from a mental perspective for developers working on projects on their own. You are not in charge for the server that powers your application, so you are not on call 24/7 to fix any problem that might happen to it.
You don't have to be a system administrator or devops expert to run your app.

Sounds like a dream world, where is the catch?

First, serverless is still at its very early stages. All players have a different implementation of it, and the tooling around it varies in quality.

Pricing wise, it might not make sense for you, if you have a predictable traffic and you can purchase your servers for cheaper, for example by reserving instances on AWS.

You also don't control the server, which means you have to rely on the available infrastructure for logging, monitoring and debugging, and it's difficult to reproduce your setup locally.

What are the major players in the market?

- [AWS Lambda](https://aws.amazon.com/lambda/)
- [Azure Functions](https://azure.microsoft.com/en-us/services/functions/)
- [Google Cloud Functions](https://cloud.google.com/functions/)

AWS Lambda is the most famous and used one probably, and currently allows you to create serverless functions in Java, Go, PowerShell, Node.js, C#, Python, and Ruby.

AWS Lambda is the underlying service used by products that aim to simplify the serverless offer for developers:

- [Netlify Lambda Functions](/netlify-functions/)
- [Apex Up](https://up.docs.apex.sh/)

They have an awesome FAQ on <https://aws.amazon.com/lambda/faqs/> which I recommend to read.