##Introduction

- FlexBox and grid layout are both powerful layouts.

**Flexbox:**

- Flexbox is a one-dimensional layout model and is best suited for arranging elements in a single row or a single column.
- Flexbox is particularly useful when the size of the elements or the size of the container is unknown.
- It's great for aligning items both horizontally and vertically, and it's very useful for creating navigation bars, sidebars, or toolbars.

**CSS Grid:**

- Grid is a two-dimensional layout model and is best suited for arranging elements into rows and columns at the same time.
- It's great for creating complex layouts and can handle both columns and rows simultaneously, which makes it a good choice for building complex page layouts.

**Grid layout In detail**


``` CSS
grid-template-columns: repeat(3, 1fr);
grid-template-row: repeat(3, auto);
grid-column: 1/3
grid-row: 1/4
```

**Row Overriding**

- The repeat(3, minmax(200px, 1fr)) statement creates three rows (or columns, depending on where it's used), each with a minimum size of 200px and a maximum size of 1fr.
-  The 1fr unit represents a fraction of the available space in the grid container. So, if the container's size exceeds the total minimum size of all rows (600px in this case), the remaining space will be distributed equally among the rows.

``` CSS
repeat(3, minmax(200px 1fr))
```

**auto-fit & auto-fill**

The auto-fill and auto-fit keywords in CSS Grid control how the grid behaves when the grid items don't take up extra space in the grid container.

**auto-fill**

``` CSS
.container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
}
```
In this example, the grid will create as many 100px columns as it can fit in the container. **If there's space left over, it will be distributed equally among the columns.**

**auto-fit:** 

- This keyword also tells the grid to create as many tracks as possible, but it collapses the empty tracks, so there are no empty tracks at the end of the grid.

``` CSS
.container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
}
```
In this example, the grid will create as many 100px columns as it can fit in the container. **If there's space left over, it will be distributed equally among the columns, and any empty columns will be collapsed.**

**subgrid**

- The subgrid value in CSS Grid Layout is used when you want a grid item to become a grid container and align with its parent grid.

``` CSS
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}

.item {
  display: grid;
  grid-template-columns: subgrid;
}
```

NOTE:-
- This can be useful when you want nested grids to align with the parent grid.
- However, subgrid is not widely supported in all browsers.


**Container Query**

1. Container Size query

- Width Media queries consider the viewport width
 but container size queries consider the container width Containers are the elements being queried. 

**Rules:-**

- Rules with in effect only the container descendants **not the container itself**

- container size queries are an addition to responsive design not a replacement for media queries.

``` html
<article class="card">
    <h2>That's No Moon. It's a Space Station.</h2>
    <p class="text">At 198km diameter, Mimas is bigger than the first Death Star (120km) but smaller than the second (800km). </p>
    <p class="link"><a href="https://science.nasa.gov/saturn/moons/mimas/" target="_blank" class="button">More about Mimas</a></p>
  </article>

<!-- we can't query cards in container query so only work with descendants-->
<!-- Workaround solution would be check below-->
<div class="card">
<article >
    <h2>That's No Moon. It's a Space Station.</h2>
    <p class="text">At 198km diameter, Mimas is bigger than the first Death Star (120km) but smaller than the second (800km). </p>
    <p class="link"><a href="https://science.nasa.gov/saturn/moons/mimas/" target="_blank" class="button">More about Mimas</a></p>
  </article>
</div>

.card {
  container-name: card;
  container-type: inline-size;
}

@container card (min-width: 200px) {
  article {
    background-color: red;
  }
}

@container card (min-width: 250px) {
  article {
    ...
  }
}
```
