---
title: Express Templates
description: "Express is capable of handling server-side template engines. Template engines allow us to add data to a view, and generate HTML dynamically."
date: 2018-08-30T07:00:00+02:00
booktitle: "Express"
tags: express
tags_weight: 5
path: express-templating
---

Express is capable of handling server-side template engines.

Template engines allow us to add data to a view, and generate HTML dynamically.

Express uses Jade as the default. Jade is the old version of Pug, specifically Pug 1.0.

> The name was changed from Jade to Pug due to a trademark issue in 2016, when the project released version 2. You can still use Jade, aka Pug 1.0, but going forward, it's best to use Pug 2.0

Although the last version of Jade is 3 years old (at the time of writing, summer 2018), it's still the default in Express for backward compatibility reasons.

In any new project, you should use Pug or another engine of your choice. The official site of Pug is <https://pugjs.org/>.

You can use many different template engines, including Pug, Handlebars, Mustache, EJS and more.

## Using Pug

To use Pug we must first install it:

```bash
npm install pug
```

and when initializing the Express app, we need to set it:

```js
const express = require('express')
const app = express()
app.set('view engine', 'pug')
```

We can now start writing our templates in `.pug` files.

Create an about view:

```js
app.get('/about', (req, res) => {
  res.render('about')
})
```

and the template in `views/about.pug`:

```pug
p Hello from Flavio
```

This template will create a `p` tag with the content `Hello from Flavio`.

You can interpolate a variable using

```js
app.get('/about', (req, res) => {
  res.render('about', { name: 'Flavio' })
})
```

```pug
p Hello from #{name}
```

This is a very short introduction to Pug, in the context of using it with Express. Look at the [Pug guide](https://flaviocopes.com/pug) for more information on how to use Pug.

If you are used to template engines that use HTML and interpolate variables, like Handlebars (described next), you might run into issues, especially when you need to convert existing HTML to Pug. This online converter from HTML to Jade (which is very similar, but a little different than Pug) will be  a great help: <https://jsonformatter.org/html-to-jade>

> Also see the [differences between Jade and Pug](https://pugjs.org/api/migration-v2.html)

## Using Handlebars

Let's try and use Handlebars instead of Pug.

You can install it using `npm install hbs`.

Put an `about.hbs` template file in the `views/` folder:

```
Hello from {{name}}
```

and then use this Express configuration to serve it on `/about`:

```js
const express = require('express')
const app = express()
const hbs = require('hbs')

app.set('view engine', 'hbs')
app.set('views', path.join(__dirname, 'views'))

app.get('/about', (req, res) => {
  res.render('about', { name: 'Flavio' })
})

app.listen(3000, () => console.log('Server ready'))
```

You can also **render a React application server-side**, using the [`express-react-views`](https://github.com/reactjs/express-react-views) package.

Start with `npm install express-react-views react react-dom`.

Now instead of requiring `hbs` we require `express-react-views` and use that as the engine, using `jsx` files:

```js
const express = require('express')
const app = express()

app.set('view engine', 'jsx')
app.engine('jsx', require('express-react-views').createEngine())

app.get('/about', (req, res) => {
  res.render('about', { name: 'Flavio' })
})

app.listen(3000, () => console.log('Server ready'))
```

Just put an `about.jsx` file in `views/`, and calling `/about` should present you an "Hello from Flavio" string:

```js
const React = require('react')

class HelloMessage extends React.Component {
  render() {
    return <div>Hello from {this.props.name}</div>
  }
}

module.exports = HelloMessage
```
