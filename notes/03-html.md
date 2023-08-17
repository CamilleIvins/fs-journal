# HTML



#Figma
www.figma.com
design philosophy
frames, boxes, pens to sketch out the grouping of prospective elements
* also allow for screen/desktop screen sizes
industry standard tool
#16161D = "color you see when you close your eyes"

Sam's Aug 10th lecture - Figma to dev

powershell it out --> touch index.html style.css
HTML -- !
TEST: throw element on page and bcw-serve - see if the element shows up
**LINK stylesheet <link rel="stylesheet" href="style.css">
AND Bootstrap and MDI
**ANCHOR - place your stylesheet LAST in the list
TEST CSS: color element

Lock, rock, roll

Dev out low-fidelity version first - get the basic elements where they out to be in HTML
**color code containers, rows, columns - outline all elements, see notes
^Bootstrap grid system

Now, code-wise: <header>, <main>, <footer>
class="container-fluid" <-- because we will be moving items along the flex
 for each: h, m, f
container = span across 100% viewport
container-fluid = little bit of margin

<section> class="row" -- tags for rows = 4 -- 3 in main, 1 in footer

**NOTE - accommodate mobile considerations early, fix for desktop later, easier to scale up** Mobile-first design

**NOTE - type in filler words so grid shows up in web view

<div> class="col-n" MF-D = col-md-6 adjusts for desktop up
Bootstrap gris system already wraps w/in "row" class, exceed 12 rows? --> auto wrap to next line

<footer> mobile default col-12 elements auto stack on each other, desktop -- both ends
so col-12 col-md-col-6

**LINK - BCW snippets debug style tag
"Debug Style Tag"
type: style:debug (tab) add class to HTML debug
**NOTE -  make sure to add the debug class to your body to see the borders from the style tag above

ADD notes to code to designate section - anchor notes, Ahoy!
ie
**SECTION - banner

**NOTE - use web view element selector to see what is going on with regard to rows and such
ie -- want center?
<section> "row justify-content-center"
 refresh page and then look elem
 Have text? go to column and center the text w/in
 <div> "col-12 col-md-3 text-center"
w/in (<div>) place <h1> Text </h1> (<div>)

justify-content moves upon x-axis
align-content moves along y
UNLESS
you flex column- or row-reverse
THEN flip

**LINK - css-tricks.com/snippet/css/

use dev tools to mess with element height to see what things will look like with change in height - ie is element centered along y-axis


use special classes to hold elem in spots during blueprint mock
ie. set viewheight (vh) to 500px

use basic bg-_____ to put elem in backgrounds of their own against sections
**NOTE - you like pastels
 even bg <div> elems to set apart w/in the general <section>

 **NOTE - rows have negative (-) margin, col have padding
 adding margin on col? adds affitional space w/in row = break the 12unit base of rows

 DO NOT treat your col as cards, w/in col make your elemes/cards

 **NOTE - col designate area for item, not item itself

 **ANCHOR - ctrl+D to highlight and replace multiple things

 <section> "row justify-content-center"
 refresh page and then look elem
 Have text? go to column and center the text w/in
 <div> "col-6 col-md-3 p-4" <div class=bg__> Text</div> </div>

 **STUB - align-content is not for d-flex, use align-items(-center or -start)

**NOTE - be mindful of inheritance

<footer class = container-fluid

<S class= row
<d col-12 col-md-6 text-center text-md-start
<p> Text

<d col-12 col-md-6 text-center text-md-end
<p> Text

**STUB - <p> have margin built in, so style above default
css =
p {
    margin: 0
}

see changes in dev tools in real time

When needed, grab values from Figma

:root = pseudoclass == global variable you can reference WITHIN other classes
root specifically houses variables

<!-- utility classes -->

take priciple of bootstrap - which is utility classes bundled, haha

ie
.bg-green {
    background-color: var(from the :root pseudo)
}

**NOTE - YOUR CSS will override BS, if not, type !important to override
esp their color classes are stacked with !important, overriding our class, unless we !important over it, otherwise,by specificity count, you will lose to bootstrap.

easiest is to gen own naming, so as to not have to override

move classes that you can to a custom class to clean HTML
ie justify-content-center, align-items-center


background-position is best for styling bg images
cover - fits longest axis
contain - all image and tesselate

div inside of div to make cards - bundle all the elements
p tag and button w/in
padding spaces w/in = good for text not reaching ends of their boxes
putting class w/in a button manipulates content in button, need to wrap it in another box to get padding 
button now in full div row space
d --> button
same with images

in-line - exists w/in itself
vs
block - p-tag - block around

read MDN to know more!!!

**FIXME - "rounded-pill" = class you were looking for

cannot use bootstrap shortcuts into your own, separate stylesheet, but this will let you have more control
OTHERWISE you need SCSS or SASS, which is above our station

backdrop-filter: blur

**ANCHOR - Spice time
start with one container card

<d class> rounded
<img src=""> rounded-top img-asdf
<d class> bg- text-white tp-3 rounded-bottom
<p ham> rounded bottom
<button class= "bg- rounded-pill w-50 p-2  fs-##"> + <i class>
custom class
.img-asdf{
    h:20vh
    w:100%
}

**ANCHOR - css-tricks.com/absolute-relative-fixed-positioning-how-do-they-differ

css-tricks.com/absolute-positioning-inside-relative-positioning

HTML is top down, respects parent elem
position absolute = no longer respect outer structure of HTML nesting
 ie

 .btn-asddf{
 position: absolute

 }

 now elem is indep on page relative to all other elements
 *******
 Does not work w/o reference to a relative element
 No listed relative elem = to whole page, hence, relative to entire doc
 Must make relative to the div

 So reassign the hierarchy of the elements --> make a new closest relative element
 make button relative to x container

  .container-asddf{
 position: relative;
 display: flex;
  }

 NOW

  .btn-asddf{
 position: absolute
 bottom: 5px;
 }


 **NOTE - could have many position: relative BUT the closest relative element will be the one to become the reference point!!!

  .container-asddf{
 position: relative;
 display: flex;
 flex-direction: column;
 align-items: center  <----because you changes the flex dir, not justify
 }

 NOW

  .btn-asddf{
 position: absolute
 bottom: 5px;
 
 }

 add custom media queries to alt
 on this screen sixe apply x CSS and on this screen size apply y CSS
 @media
^based on min screen width
        768px is the md breakpoint
**NOTE - can ref as many classes or selectors as we want w/in one media query - cand do for every size, FOR EVERY CSS rule you've written
^ still add breakpoint, or set at max-width to base case desktop, base case mobile is min-width

@media (min-width: 768px) {
.card-something{
    background-img: url() <-- can ref other class and replace at a specific breakpoint
}
}

Custom font, sticky nav bar
sticky-top sticks to the top of the thing above it ie, if you scroll away from header, you lose it

<header class="sticky-top" ><-- keeps section to top of viewport js adds transition

add font type to utility calsses
.font-name {
    font-family: 'name', stylization
}

button {
    box-shadow: px px px px, color
    border:
}

https://www.figma.com/file/YleNmJbuGPUlSU5krdeM1R/Green-Eggs-and-Ham?type=design&node-id=1%3A18&mode=design&t=wSRrmf7AHwHHf8tR-1

