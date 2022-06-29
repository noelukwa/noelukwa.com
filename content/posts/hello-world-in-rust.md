---
title: 'Writing Http Handlers in Go'
date: 2022-01-04T10:50:13+01:00
draft: false
---

When writing web services in go, more often than not you are basically mapping routes to handlers which in turn could contain all the logic required to handle the incoming request or make calls to other functions, if you are familiar with some mvc frameworks such as expressjs, then you must have written and to handle the incoming requests. In go, our controllers are s, and our router is .

Lets look at an example of a simple http handler.

```go {linenos=true}
package main

  import (
    "net/http"
    "fmt"
  )

  func hello(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello World!")
  }

  func main() {
    http.HandleFunc("/", hello)
    http.ListenAndServe(":8080", nil)
  }
```

Ok? soo where's our handler and where's our router? and whats that ServeHTTP method all about? 😱.

In order to understand the above code clearly, we need to understand one thing first and that's In simple terms, assume that your go codebase is just a community of many gangs, each gang has a handbook that defines how anyone who wishes to be a member should In this case, the gang is named and the handbook specifies that who ever wishes to belong must have a method
In order to have a complete request handler, we need a router aka and thats exactly what the http.Handle method does. Lets take a pause for a moment and imagine we have over 10 different handlers, and we want to map them to different routes, it will be really counter intuitive to create a custom handler and have all of them implement ServeHTTP, Well, we can actually use regular functions passing in But remember we need to implement the "ServerHTTP" method in order to be a valid handler, in this case we're still doing that but we'll leave the implementation of ServeHTTP to a built in type and focus on writing just functions.

Here's how http.HandlerFunc works:

Basically it's an [adapter](https://golangbyexample.com/adapter-design-pattern-go/) that allows us to use regular functions as handlers.

If you noticed, there's still a handful of repetition going on in our example above, we can abstract that away by using another function.

Earlier i said that handlers are like our controllers and ServeMux is our router, but we haven't defined any "router" explicitly anywhere, that's because we're using the default one, which is http.DefaultServeMux. Which you shouldn't use in any serious application.

Here's how we can define our own router and use it:

That's basically it for handling http requests in golang, however we can still improve on the in built methods by using some open source routers that adds more functionalities to the default ServeMux such as matching based on the method.

Here are some of the open source routers that we can use:

- [gorilla/mux](https://github.com/gorilla/mux)
- [echo](https://github.com/labstack/echo)
- [httprouter](https://github.com/julienschmidt/httprouter)
- [chi](https://github.com/go-chi/chi)

Alright! that's it pal! go on and build.
