**How HTML renders in our pages**

1. Browser Loads HTML
2. Converts HTML into DOM
3. Feching Linked Resources
4. Browser parses CSS (CSSOM)
5. Combine DOM with CSSOM
6. UI is painted (FCP) (First Contentful Paint)


HTML types of Element

primarily

 1. Block Level
 2. InLine

**CSS Selectors:-**

 1. type/Attribute Selector
 2. Class selector
 3. Id Selector
 4. Universal Selector (*)

**CSS Inheritance**

It occurs when an inheritance CSS property (i.e color) is not set directly on an element, the parent chain is traversed until a value for that property is found.

``` html
<div class="body">
	<p>This is a Paragraph, but it will have the blue color due to inheritance</p>
</div>
<style>
.body{
	color: blue;
}
</style>
```
**case 2**

``` html
<div class="body">
	<p>This is a Paragraph, but it will have the red color due to direct Specification</p>
</div>
<style>
p {
color: red;
}
.body{
	color: blue;
}
</style>
```

**case 3**

``` html
<div class="body">
	<p>This is a Paragraph, but it will have the blue color due to strong Specification</p>
</div>
<style>
p {
color: red;
}
.body p{
	color: blue;
}
</style>
```

**What is CSS Specificity**

1. the algorithm used by browsers to determine which css declaration should be applied.
2. Each selector has a calculated weight. The Most specific weight wins.
                     id--class -type
Id Selector: 1 - 0 - 0
class selector: 0- 1 -0
type selector: 0-0-1

NOTE:- Inline Css are more specificity and **!import** has even more specificity

[Css Specificity Calculator](https://specificity.keegan.st/)

**Em & Rem**

**EM:- relative to its parent font-side**

``` html
<html>
<div>
<p></p>
</div>
</html>

<style>
html {
	font-size: 16px;
}

div {
font-size: 2em; //16px * 2 = 32px;
}

p {
font-size: 2em; // 32px * 2 = 64px
}
</style>
```
**REM:- relative to Root font-side**

``` html
<html>
<div>
<p></p>
</div>
</html>

<style>
html {
	font-size: 16px;
}

div {
font-size: 2rem; //16px * 2 = 32px;
}

p {
font-size: 2rem; // 16px * 2 = 32px
}
</style>
```

%:- % calculation

``` html
<html>
<div>
<p></p>
</div>
</html>

<style>
html {
	font-size: 16px;
}

div {
font-size: 120%; //1.2*16 = 19.2px;
}

p {
font-size: 120%; // 1.2 * 19.2 = 23.04px
}
</style>
```

**CSS Combinators**

1.Descendent Selector (**ul li a**)

``` HTML
<ul>
<li><a href='#'></a></li>
</ul>
```
2.Child Combinators (direct Descendant) (**div.text > p**)

```HTML
<div>
<div class="text">
   <P>Here the CSS will apply<P>
</div>
<div>
  <p>No CSS will apply</p>
</div>
</div>
```

3.Adjacent Sibling Combinator (**h1 + p**)

Note:-
1. Both h1 and p should be in the same parent
and p should be immediately after the h1 tag

4.General Sibling Combinator (**p ~ code**)


Note:-

1. they should not have an immediate sibling like an adjacent sibling. But they must have siblings
2. They must have the same parent


**Block Element Modifier Architechure(BEM)**

1. Design Methodology that helps create reusable components and code-sharing

**Other Methodologies**

1. OOCSS
2. SMACSS
3. SUITCVSS
4. ATOMIC
5. BEM


**Block**

1. header
2. Menu
3. input
4. checkbox (stand alone meaning)

**Element** (part of block)

1. Menu items
2. List Items
3. Header title

**Modifier**

1. Disabled
2. highlighted
3. checked
4. Yellow

**.block__element--modifier** Syntax

``` HTML
<form class=form>
   <input class='form__input'/>
   <input class="form__input form__input--disabled"/>
   <button class="form__button form__button--large"/>
</form>
```


**Box Model:-**

![Box Model layouts](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/6n3nl1gs9enf16a1g3nn.png)


``` CSS
.box{
width: 200px;
height: 80px;
padding: 20px;
border: 10px;
}
// Here the actual size of the box is 
height = 140px;
width = 260px;
```

**Box-Sizing: border-box;**
 When we add this we are saying HTML compiler that whatever we specify the height and width that should be it.

if there is padding and border you need to align it internally. but my width and height should not exceed the mentioned size.

``` CSS
.box{
width: 200px;
height: 80px;
padding: 20px;
border: 10px;
box-sizing: border-box;
}
// Here the actual size of the box is mow
height = 20px;
width = 140px;
```


**Position**

It is the most confusing topic, hope I will make it clear to you 

- static
   - Element is positioned according to the normal flow of the document.
   - Top right bottom and left
- relative
   - Element is positioned according to the normal flow of the document but offset relative to its normal positioning
   - Based on Top right bottom and left 
- absolute
   - Element is removed from normal document flow
   - Positioned relative to closest positioned ancestor
   - Top right bottom and left (based on)
- fixed
   - Element is removed from Normal Document flow
   - Position Relative to the containing block established by view port
   - Top right bottom and left 
- sticky
  - Element is positioned according to normal document flow then offset relative to nearest scrolling ansestor.
- Top right bottom and left

**Visualization of fixed and sticky is very crucial **

https://css-tricks.com/almanac/properties/p/position/

**DropShadow**


![Drop Shadow Example](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/6qlj0vm410q2y96aht0s.png)


## Pseudo Classes

**Input-Element pseudo-classes**

- :enabled
- :disabled
- :checked
- :required
- :optional


**Location pseudo-classes**

- :any-link
- :link
- :visited 

**Tree Structure pseudo-classes**

- :root
- :nth-child()
- :first-child
- :last-child

**User Action pseudo-classes**

- :hover
- :active
- :focus

**Functional pseudo-classes**

- :is()
- :not()


## Pseudo Elements

- ::before
- ::after
- ::placeholder
- ::first-line


**Reference**

https://frontendmasters.com/courses/css-foundations
