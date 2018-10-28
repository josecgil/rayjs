# Ray.JS

`ray.js` is a library that checks the DOM for html components and execute its related js counterpart

![alt tag](https://raw.githubusercontent.com/josecgil/rayjs/master/logo/rayjs.jpg)

## Table of contents

1. [Installation](#installation)
2. [An overview](#an-overview)
3. [Errors](#errors)
4. [More examples](#more-examples)

## Installation

Just download [ray.js](https://raw.githubusercontent.com/josecgil/rayjs/master/dist/ray.js) and load it in your page

or use this:

```<script type="text/javascript" src="https://raw.githubusercontent.com/josecgil/rayjs/master/dist/ray-min.js"></script>```

then, when your are ready to start looking for components, execute this:

```
<script type="text/javascript">
    new Ray().begin();
</script>
```

## An overview

When de DOM is ready `Ray.js` checks the DOM for elements with the `data-ray-component` attribute and executes the js that indicates the value of this attribute.

Example:

Let's suppose we have this html (note the `data-ray-component` attribute)

```
    <img data-ray-component="ChangeImageSrcComponent" src="images/test1.jpg">
```

the JS part of this component changes the src when it's executed:

```
    window.ChangeImageSrcComponent=function(data) {
        var image=data.DOMElement;
        image.setAttribute("src","images/test2.jpg");
    };
```
For a more complex example check the [samples directory](https://github.com/josecgil/rayjs/tree/master/Samples)

## Data object

On every execution an component ```ray.js``` injects a data object containing 2 properties:

* DOMElement: a reference to the DOMElement that triggers the execution of the component
* bus: a reference to an EventBus

## EventBus

The ```ray.js``` EventBus has two methods:

* ```trigger(eventName, eventPayload)``` triggers an event with the corresponding payload
* ```on(eventName, callbackFn)``` listen to an event an sets the callback function to be called when the event happens

## Errors

```ray.js``` throws an "ray.error" event on the EventBus if it detects an Error with the Exception as the payload. You can catch the error with this sample code:
```
    ray.eventBus.on("ray.error", function(exception) {
        console.log("Error:"+exception.message);
    };
```

## More examples

You can check more complex examples in the [samples directory](https://github.com/josecgil/rayjs/tree/master/Samples)
