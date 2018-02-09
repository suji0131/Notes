# CSS Layout
[Source](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox)

## Normal Layout Flow
Normal flow is how the browser lays out HTML pages by default when you do nothing to control page layout (elements stacked up on top of one another).

## Floats
***float*** property has 4 possible values: **left**, **right**, **none**(default), **inherit**

## Positioning

## Flexbox
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














