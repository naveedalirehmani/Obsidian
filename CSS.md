### Selectors.

X[href^="https"] if starts with https 
X[href*="foo"] by attribute and string anywhere in the value 
X[href="foo"] by attribute and it's value 
X[title] by attribute 
X ~ Y all proceding elements 
X > Y all first children 
X + Y preceding sibling 
a:visited and a:link clicked and yet to be clicked. 
input[type=radio] :checked type=radio and is checked 
X::after X::before you know this :) 
div:not(#container) all divs except one with id=container 
*:not(p) every element except p tag 
p:first-line & p:first-letter self explanatory :) 

X:nth-child(n) & X:nth-last-child(n) & X:nth-child(2n) nth-child / nth-child from last / every 2 child X:first-of-type first child of it's type 
div:has(p) all divs that contain p tag / in css we can select next sibling or children but select previuos elements or parents through children is hard. this makes it possible / this is very power selector

---
### Grid

Grid-template-row : define rows by size in px;
Grid-template-column : define columns by size in px;

---

grid-row-start
grid-row-end
grid-col-start
gird-col-end

Grid-row : row-state/row-end;
Grid-column : column-start/column-end;

Grid-area : row-start / col-start / row-end / row-end;

---

Fr and minmax(100px, 3fr)
repeat(3,1fr)

Grip-gap : 1rem
Grid-gap : 1rem 2rem; //rows and then columns  
  
if a grid item is 100px * 100px and the content is 10px by 10px you can also use justify-items and align-items just like flex. To align each content inside of a grid item  
if you are using grid inside of a parent div, you can also align the whole grid with justify-content and align-content in the parent div.

Special : repeat(auto-fit, minmax(100px, 200px))

Grid-auto-rows : 100px; // sizing for implicitly added grid-items;
Grid-auto-columns : 100px; // same as above
Grid-auto-flow : column // this will add implicitly added items to grid in new columns, by default is rows


