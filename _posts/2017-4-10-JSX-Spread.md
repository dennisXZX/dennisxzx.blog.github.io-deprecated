---
layout: post
title: JSX Spread Attribute
tags: [react]
---

Say you want to pass all the properties of an object down to a child component, what you would normally do is something like:
```
<ShowCard key={show.imdbID}
          poster={show.poster}
          title={show.title}
          year={show.year}
          description={show.description} />
```
With the `...` spread operator specific for JSX, you can deconstruct the object and pass all the properties in one go.
```
<ShowCard key={show.imdbID}
          {...show} />
```
However, this inexplicit approach has two disadvantages:

- it would pass everything down to the child component, some of the properties might not be relevant to it.
- it's making the code slightly difficult to read.

So personally I would always prefer to go for the explicit approach, but we have to keep in mind the existence of the spread operator.