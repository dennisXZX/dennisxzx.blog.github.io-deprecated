---
layout: post
title: Log Helper Function
---
Logging something out to console is a classic way to debug your program. I bumped into a situation today where I need to log out a message in an array chain. 

In the following code, we first filter an array and then apply a map function to the filtered array. Sometimes we want to log out the filtered array to see if it works as we expect.
```
// helper function to log out the array
printOnceFactory() {
    let isPrinted = false;
    return function(x, index, arr) {
        if(!isPrinted) {
            console.log(arr);
            isPrinted = true;
        }
        return x;
    }
}

preload.shows
    // filter the shows array to include only those that match the search term
    .filter((show) => {
        return (
            show.title.toUpperCase().indexOf(this.state.searchTerm.toUpperCase()) >= 0
        )
    }).map(this.printOnceFactory()) // log out the filtered array
    // map the array to a JSX array
    .map((show) => {
        return (
            <ShowCard show={show} key={show.imdbID} />
        )
    })
```