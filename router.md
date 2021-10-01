# Kata: Router

We're going to build a router as you might find in a web framework like Express, Django or NextJS.

What does routing do? In essence it matches given path with a route, and then invokes a function associated with that route. Some
information can be extracted from the path which is then passed along to this function.

So if we have the route `/user/:id` it would match the path `/user/martijn` and extract the id `martijn` from it. This route
also has a function associated with it that is called with the extracted id.
This function then returns something, for instance some JSON or some HTML. In a real world routing scenario often more information
is passed along to this function, like a request object that represents a HTTP request.

## A hardcoded router

Create a match function that matches a single route, `/first`. It takes a single argument, the path. When passed in a path 
`/first` it should match and return true. If passed something else it should return false.

```
match('/first') --> true
match('/other') --> false
```

Do not worry about patterns like `/users:id` yet at this point. We'll get to them later.

## A configurable router

A hard-coded router above is not very useful. So let's make the router configurable. Extend the match function so that it
receives a new first argument that has the list of expected routes.

```
match(['/first', '/second'], '/first') --> true
match(['/first', '/second'], '/second') --> true
match(['/first', '/second'], '/other') --> false
```

## Matching a route to a value

Our match function above tells us that a route matches or not, but it doesn't tell us which route matched: we cannot attach
a value to a route. We want to modify the match function so that we can associate a value with a route, and return that value
if there is a match:

```
routes = [{route: '/first', value: 1}, {route: '/second', value: 2}] 
match(routes, '/first') --> 1
match(routes, '/second') --> 2
match(routes, '/other') --> null
```

## Resolve a route

Now we can use the above `match` function to implement a `resolve` function. This should, when given a path that matches the route, 
call the function associated with the route. In this example, we have a function `hello` that when called returns the value "Hello!".

```
routes = [{route: '/first', value: hello}]
resolve(routes, '/first') -> "Hello!"
```

## route patterns

You may have already wanted to implement pattern matching for `/user/:id`. Now is your chance!

Let's go into the rules for these variables first. Instead of a hardcoded step, we can instead indicate a step is 
a variable with the prefix `:`. The whole step then becomes a value, so that `/user/martijn` matches, but `/martijn` does not,
and neither does `/user/martijn/edit`, as the step `edit` is not part of the route pattern.

Do not worry about the value of variables like `:id` yet.

Extend it with a route that takes more than a single variable, like `/user/:id/property/:name`.

## route precedence

What if we have a route `/user/martijn` *and* a route `/user/:id`? If we now resolve the path `/user/martijn`, which one wins? 
The simplest way is to let the route that comes earlier in the routes list win. Make sure you have a test for this!

## Pass the variables along

Now we want a version of the `hello` function that greets people by the variable `id`, like "Hello martijn!". We also
want to supports routes that have multiple variables. What would be a good way to get the variables from the route into the function?

## Hook it up to the web

Let's see about hooking our router up to the real web. For now, whatever we return has the `Content-Type` of `text/plain`.
 
To make this work we need some kind of basic web server setup that lets us handle a HTTP request and return a HTTP response. For
Python, [WebOb](https://webob.org/) is a good starting point. For NodeJS you can use the built-in [http module](https://nodejs.org/en/docs/guides/anatomy-of-an-http-transaction/).
We can then plug our router into it. Your favorite programming language almost certainly has a HTTP server implementation you
can use!

Do think about testing! We're not concerned with full integration tests and thus not interested in testing the HTTP handling
itself, but we do want to test as much of the integration as possible. How would we go about that?

## HTML and JSON

Instead of plain text, return some HTML (`text/html`) or JSON (`application/json`). How do we make it so we can control
what type is returned from the function we route to? How do we make it convenient to return JSON without serializing it separately
in each function?

Congratulations: you're well on the way to writing your own web framework!

## Bonus: handling URL parameters

Make it so that you not only pass path variables (like `id` in `/user/:id`) into the routing functions, but also any parameters attached to the path
like `/first?a=1&b=foo`. How would you parse this structure, and into what? What about repeating variable names (which are allowed in URLs)?
Hint: you're not on your own. Look for library code to help you!