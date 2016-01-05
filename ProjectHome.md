**warning: this is an early prototype, use for proof of concept only**

jFunk will allow you to retrieve (and soon, manipulate) objects within complex JSON or Javascript objects.  The design of the jFunk API will closely parallel the jQuery API, replicating it exactly except where the differences between DOM and Javascript make replication nonsensical.

The current script is in an extremely rudimentary, throwaway prototype form, provided simply for exploratory purposes.

  * I would not recommend trying jFunk unless you are familiar with jQuery, otherwise this will not make much sense

  * This will only be appropriate with deep, complex Javascript/JSON structures

  * It has no expectation of good performance

  * The code is not "designed" currently, simply cowboy coded until it did some useful proof of concept things.  So its ugly, and probably buggy!

  * It does not avoid looping structures, if a parent contains a child which contains a reference to it's parent, a loop will occur and lock your browser!

However, depending on level of interest and available time, a properly architected version will be written.

So far, only these selectors are supported:

```
    *
    name[atr]
    name[atr=val]
    name:first
    name:last
    #id
    .class
    parent > child
```
It is recommended that you always use > between known parents and their direct children, to avoid unnecessary deep searching.

Some examples of use:
```
var Food={
    fruits: [
        { name: "Banana", color: "Yellow" },
        { name: "Apple", color: "Red" },
        { name: "Grapefruit", color: "Orange" },
        { name: "Kiwi", color: "Green" }
        ],
    vegetables: [
        { name: "Carrot", color: "Orange" },
        { name: "Turnip", color: "Purple" },
        { name: "Rutabaga", color: "Yellow" },
        { name: "Sweet Potato", color: "Orange" }
        ]
    };

var orangeStuff=jF("*[color=Orange]",Food).get();
var orangeVeg  =Jf("> vegetables > *[color=Orange]",Food).get();

//orange stuff is now [{name:"Grapefruit",color:"Orange"},{name:"Carrot",color:"Orange"},{name:"Sweet Potato",color:"Orange"}]
//orange veg is now [{name:"Carrot",color:"Orange"},{name:"Sweet Potato",color:"Orange"}]

```
