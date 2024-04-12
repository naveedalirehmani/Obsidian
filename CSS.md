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
