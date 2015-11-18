# Intro CSS

## Breakdown of Syntax

Every CSS statement will always include a `selector` and a `declaration`, which together is known as a rule-set or simply a `rule`. Phrased another way, a rule equals the combination of a selector and a declaration.

**Example CSS Rule:**
![CSS prototype](https://en-support.files.wordpress.com/2011/09/css-selectors-lrg.png)

The `selector` labelled `a` is the targeted html tag that will be altered with the property and value.

This means that all anchor, `a`, html tags will be affected with whatever is inside the declartion brackets: `{` and `}`. As you can probably deduce, the background color of the `a` tags will become the color `yellow` since in the declaration, the property and value are respectively `background-color` and  `yellow`.

## Requiring Stylesheets

**The Best Way** - External (css lives in a separate file).

```html
<html>
<head>
    <title>I like clean code</title>
    <link rel="stylesheet" href="css/styles.css">
</head>
<body>
    <p></p>
    <p></p>
</body>
</html>
```


```css
p {
    font-size: 14px;
}
```

**The Lazy Way** - Internal

```html
<html>
<head>
    <title>I feel lazy</title>
    <style type="text/css">
        p {
            font-size: 14px;
        }
    </style>
</head>
<body>
    <p></p>
    <p></p>
</body>
</html>
```

**The Worst Way** - Inline

Note: this is what chrome does when you add styles from the elements tab in your console. This is also how javascript applies css to elements.

```html
<html>
<head>
    <title>I am a terrible person</title>
</head>
<body>
    <p style="font-size:14px;"></p>
    <p style="font-size:14px;"></p>
</body>
</html>
```

*Take away*

"Seperation of Concerns" is a best practice.

* HTML does Structure / CSS does Layout / JS does interaction
* Less code repetition
* Easier to read / organize / refactor

## Specificity of Styles

Given the following html:

```html
  <p class="pick-me" id="pick-me">What color am I?</p>
```

Which color wins? Round 1.

```css
  p {
     color: red;
     color: green;
  }
  
  p {
     color: blue;
  }
```

Which color wins? Round 2.

```css
  html body p {
     color: orange;
  }
  
  #pick-me {
     color: blue;
  }
  
  .pick-me {
     color: green;
  }
  
  p#pick-me.pick_me {
     color: red;
  }
  
  p.pick-me {
     color: yellow;
  }
```

Which color wins? Round 3.

```css
  #pick-me {
     color: blue;
  }
  
  p#pick-me {
     color: orange;
  }
  
  p {
      color: red !important;
  }
```


Solutions:

1. blue beats green beats red.
1. red beats blue beats yellow beats green beats red beets oranges bananas.
1. red beats orange beats blue.


###The rules of CSS Specificity:

* Lower css rules / declarations overwrite higher ones.
* More *specific* selectors beat less specific ones
    * id > class > tag
        * no number of tags can beat a class
        * no number of classes can beat an id
* Inline styles > Internal styles > External styles 
* `!important` trumps all of the above.


## Inheritance of Styles


```html
    <h1>Cheese Sale! <button>Buy Now!</button></h1>
    <p>We are selling cheese.</p>
    <div class="info-box">
        <h1>Sorry!</h1>
        <p>We're out of cheese.</p>
        <button>Complain</button>
    </div>
```

```css
  h1 {
    color: blue;
  }
  
  .info-box {
    color: orange;
  }
  
  button {
    color: inherit;
  }
```

**Exercise**

What color is...

1. "Cheese Sale"?
1. "We are selling cheese"? 
1. "Sorry!"?
1. "We're out of cheese"?
1. "Buy Now"?
1. "Complain"?

When you've made your guesses, you can play with the code here:
[Inheritance Demo](http://codepen.io/pen/def?fork=WvvORV)

Which Properties are Inheritied? [See here.](http://www.w3.org/TR/CSS/#indices)

## Arranging elements to display properly

`span` and `div` are our bread and butter. They are the HTML equivalent of hydrogen and oxygen.

|display:|inline|block|
|-------:|-----:|----:|
|   | `span` | `div` |


More inline elements:

* a
* small
* img
  
Block elements:

* h1, h2, h3
* p
* header, nav, footer, section, aside --> all just divs by another name!

You can think of these tags as...

```
small = span + special_sauce
h1 = div + special_sauce
```

**Exercise**

Build your own:

* Make an inline element with a class of "strike" that "strikes out" the font inside of it.
* Make an inline element with a class of "keyword" that puts a thin black box around text.
* Make a block element with a class of "danger" with red font, a yellow background, and generous padding.
* Make a block element with a class of "success" with green font, and a thin gray border.


## Box Model: Everything is a box!

From outside, in:

* margin
* border
* padding
* content

![box model diagram](https://github.com/sf-wdi-21/notes/blob/master/week-01/day-3-functions+CSS/dusk-modular-css/img/box-model.png)

**Like a picture frame:**

* The painting is the content.
* The "matte board" is the padding (which allows the content to breathe).
* The frame is the border.
* And margin? Margin is the distance between one painting and the next.

![picture frame](https://github.com/sf-wdi-21/notes/blob/master/week-01/day-3-functions+CSS/dusk-modular-css/img/picture-frame.jpg)

**Content**

Content can be text, other elments, or nothing at all. The dimensions of your box depends on what you put in it, and whether or not you explicity set a `height` and `width`.


![mime in a box](https://github.com/sf-wdi-21/notes/blob/master/week-01/day-3-functions+CSS/dusk-modular-css/img/marceau-box.jpg)


## CSS Shorthands

These are equivalent:

```css
p {
    padding: 2em;
    /*padding-top: 2em;*/
    /*padding-right: 2em;*/
    /*padding-bottom: 2em;/*/
    /*padding-left: 2em;*/
         
    border: 2px solid black;
    /*border-width: 2px;*/
    /*border-style: solid;*/
    /*border-color: black;*/
}
```


##Resources

* CSS Reference - https://developer.mozilla.org/en-US/docs/Web/CSS/Reference
* CSS Properties List - https://css-tricks.com/almanac/properties/
* What are the Default CSS Values for each element as specified by the World Wide Web Consortium (W3C)? - http://www.w3.org/TR/CSS2/sample.html
* Where can I find the main CSS3 specs? - http://www.w3.org/TR/css-2010/
