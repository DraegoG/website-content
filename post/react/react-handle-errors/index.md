---
title: How to handle errors in React
date: 2019-01-23T07:00:00+02:00
description: "Best practices to handle errors in React using error boundaries"
tags: react
---

When working with a component, when any error happens inside this component code React will unmount the whole React component tree, rendering *nothing*. This is the React way of handling crashes.

You don't want errors to show up to your users. React decides to show a blank page.

However, this is just the default. Having a blank page show up is only slightly better than showing cryptic messages to users, but you should have a better way.

If you are in development mode, any error will trigger a detailed stack trace printed to the [browser DevTools](/browser-dev-tools/) console. Not in production however, of course, where you don't really want bugs printed out to your users.

In production you should intercept the errors, and show some kind of helpful message to the person using the app.

This is where *error boundaries* come into play.

With an error boundary, you isolate parts of the app and handle errors locally.

An error boundary is a React component that implements the `componentDidCatch()` lifecycle event, and wraps other components:

```js
class ErrorHandler extends React.Component {
  constructor(props) {
    super(props)
    this.state = { errorOccurred: false }
  }

  componentDidCatch(error, info) {
    this.setState({ errorOccurred: true })
    logErrorToMyService(error, info)
  }

  render() {
    return this.state.errorOccurred ? <h1>Something went wrong!</h1> : this.props.children
  }
}
```

and in a component JSX, you use it like this:

```js
<ErrorHandler>
  <SomeOtherComponent />
</ErrorHandler>
```

When an error happens inside `SomeOtherComponent` or other child components, and in the whole components subtree that they hold,  `ErrorHandler` is going to intercept it, and you can handle the error gracefully.

In the above case which is inspired by the React official documentation we have an `errorOccurred` state property that when set to true, makes the interface render the error handling UI, otherwise it renders the normal application UI tree.

Inside `componentDidCatch()` , which receives 2 arguments that describe the error, we also call `logErrorToMyService()` which is just a stub for some function that uses a service like Sentry, Roller, Airbrake or others that can log the error in a nice way for you to see, so you don't have to rely on users telling you there's an error to notice a problem.
