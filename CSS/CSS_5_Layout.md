# CSS Layout
Crib notes from this [Source](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox)

## Normal Layout Flow
Normal flow is how the browser lays out HTML pages by default when you do nothing to control page layout (elements stacked up on top of one another).

## Floats
***float*** property has 4 possible values: **left**, **right**, **none**(default), **inherit**

## Positioning

## Flexbox
If you resize the browser window, or add another element, the layout continues to work just fine.

To start with, we need to select which elements are to be laid out as flexible boxes. To do this, we set a special value of display on the parent element of the elements you want to affect.
```
/* creates equal size columns for every element in main*/
main {
  display: flex;
}
```

### Terminology
![Flex_terms](images/flex_terms.png)

- The parent element that has display: flex set on it is called the _**flex container**_.
- The items being laid out as flexible boxes inside the flex container are called _**flex items**_.
- The _**main axis**_ is the axis running in the direction the flex items are being laid out in. The start and end of this axis are called the _**main start**_ and _**main end**_.
- The _**cross axis**_ is the axis running perpendicular to main axis. The start and end of this axis are called the _**cross start**_ and _**cross end**_.


***flex-direction*** what direction main axis runs. **row, column, row-reverse**
```
/* or row (default)*/
flex-direction: column;
```
***flex-wrap*** if children are breaking out of container use this
```
flex-wrap: wrap;
```
Short hand for ***flex-direction***, ***flex-wrap*** is ***flex-flow***
```
/*order: direction wrap*/
flex-flow: row wrap;
```

### Flexible sizing of flex items
```
article {
  flex: 1;
}
```
Here we are giving each <article> element a value of 1. i.e, after padding and margin each flex item takes equal amount (value is a proportion) of space.
```
/* 3rd child takes double amt of the rest */
article:nth-of-type(3) {
  flex: 2;
}
```
```
/* Each flex item will first be given 200px of the available space. 
After that, the rest of the available space will be shared out according 
to the proportion units */
article {
  flex: 1 200px;
}
```
```
/* 3rd will have twice the rest of space */
article:nth-of-type(3) {
  flex: 2 200px;
}
```

### Horizontal and Vertical Alignment
***align-item*** controls where flex items sit on the cross axis

Values: **stretch** (default), **center**, **flex-start**, **flex-end**

***justify-content*** controls where flex items sit on the main axis

Values: **flex-start** (default), **center**,  **flex-end**, **space-around**(evenly along the main axis, with a bit of space left at either end), **space-between** is very similar to space-around except that it doesn't leave any space at either end.

### Ordering Flex items
Can be helpful in ordering items of main element
```
button:first-child {
  order: 1;
}
```
By default, all flex items have an order value of 0. Flex items with higher order values set on them will appear later in the display order than items with lower order values. (negatives are also allowed)

### Nested Flex boxes
It is perfectly ok to set a flex item to also be a flex container, so that its children are also laid out like flexible boxes. 
```
article {
  flex: 1 200px;
}

article:nth-of-type(3) {
  flex: 3 200px;
  display: flex;
  flex-flow: column;
}
```




