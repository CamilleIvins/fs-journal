# JavaScript
Week 2 notes Aug 14-18
Aug 17th notes on Scrum

# August 14th JS notes {

Get from slack, late summer github

after the usual mkdir add app.js to touch command

**LINK - est index.htlm as last time - stylesheets and BS, fonts, and MDI stuff

check js linked = console.log("js loaded")

JS is NOT an asset, so not a link
<!-- #region -->
<script src="app,js"></script>
    **NOTE - scripts are typically loaded at the end of the bodt since they take the longest to load

js is a little make your own rules a-la wild west
    - why it is popular, est many frameworks

console.log is how you get info from file to console

Rules are being called via set arguments, console.log helps check logic and math

<!-- primative data type, along with most strings <-- which must be in quotes -->
for let number = six <-- try to get titles to be as accurate as possible
all booleans (T/F), dir let = "", all numbers
<!-- js uses floats for numbers -->

strings can be in ``, '', or ""
`` strings can be broken into multiple lines - even for multiple empty lines

can access var inside console

//NOTE - no values
leaves undefined
let noValue <!-- undefined - I don't know there is no value <- something should be there and is not showing up-->
let knownNothing = null <!-- no value exists, starts with nothing being there -->
let unknownValue = undefined<!-- serves no purpose to ever write this -->


//SECTION - Reference data types <-- when passed they share the same source, when primitives are passed they only move their value to a new, separate source
<!-- arrays, store values by position (index), objects -->
let arr = ['Fiero','CObalt','Semper']
array starts at 0 <-- undefined would signal you are out of the array (vs null, where there is a gap)
let nums [1, 3, 4, 5, 7]
*can do mixed string, numbers, etc <--- must have good reason to do this

objects store data using KEY: VALUE pairs
let obj = {
 cat: 'Lupine'
 dog:'Marcuse'
 weasel: 'Schnapps'
 bird: 'Cobbles'
}

data not stored by position like in arrays, but by keys
console.log by key to get string
or obj.KEY
CANNOT have mult properties with same name

can iterate over array - as you share the value you share the ref

if micksNumber = otherNumber
separate storage

otherObj =obj
iterates over object with any change

<!-- **NOTE - YOU CAN DESTROY YOUR ORIGINAL DATA WHEN YOU CREATE A REFERENCE -->
This is the one you have saved, it is passing your own work and letting others write over it

<!-- truthy falsey <-- data types can be set in place of T/F values ie, within "if statements" can be returned as true or false -->

**SECTION - functions

Blocks of code to store and run later

function sayHello() {
    console.log('Hello there')
}
 function is saved, but only run when called

 sayHello() <--enter this in console and will run 'Hello there'

**NOTE - parameters - can use blanks for temprary variables - only exist (are accessible) for this function while it is executed
 function addNumbers(x, y){
    console.log (x + y)
 }

 addNumbers(3, 4)

 ^ returns 7

 functions pull variables that are locally scoped, global variables will make it essentialls a function for those only, need to have ability to write in the values - when invoking f(x)n you can add directly in the dev tools or console

 function addNumbers(x, y){
    console.log (x, y)
    console.log (x + y)
    return x + y <--gives back values to those who called them
 }

 Onyl relevent if you can use them from a user end, NOT JUST dev end

add button on html for interation
<!-- // #endregion -->
}
 # app time **SECTION - APP TIME

 Document Object Model = DOM

 document.getElementById('whatever-id-clicked')

let thingsClicked = ''

 function clickDino () {
    console.log('clicked dino', '🦖')
    thingsClicked += '🦖'
    let elm = document.getElementById(things-clicked)
    elm.innerText = thingsClicked
 }
 
 function clearThings() {
    thingsClicked = ''
    let elm = document.getElementById(things-clicked)
    elm.innerText = thingsClicked
 }

 **NOTE - onclick exists for ALL elements <-- does not need to be a button!!!!!

 function updateDom () {
      let elm = document.getElementById(things-clicked)
    elm.innerText = thingsClicked
 }

 NOW can swap

 function clickDino () {
    console.log('clicked dino', '🦖')
    thingsClicked += '🦖'
    updateDom()
 }
 
 function clearThings() {
    thingsClicked = ''
    updateDom()
 }

# Aug 15th *FIXME - red anchor for new day - Aug. 15th: creating arrays

 LINK ALL FILES - MDI, Bootstrap, own CSS, JS at the bottom of body in script tags
 header gets container classes, section gets row, div gets col
 Emojis are strings, need to be in quotes

 <!-- const creates a variable that cannot be overwritten (immutable) -->

 array can hold objects which hold keys - commas between {objects}

 for (let i =0; 1<array.length; i++){}
 
 To get something out of array, must use index

 console.log(array[i].name)

 OR
 let animal = animals[i] <-- only exists in for loop
 console.log(animal.name, animal.emoji)

   # *SECTION - forEach only works on arrays

 array.forEach()
 loops over an entire array for up to three arguments <-- value, index, array
 it is looking for a callback function

 f(x)ns are data types, and can pass for arguments

 function hello() {
    console.log('sup')
 }
 function justDoIt(fn) {
    fn()
    fn()
    fn()
 }

 justDoIt(hello)

^code runs 'sup' thrice
<!-- jusDoIt(hello()) will return hello console.log('sup')-->

values passed down, f(x)n will pass down value, even with changing the title of const variable

for (let i =0; 1<array.length; i++){
    let animal = animals[i]

    whatsGood(animal) <---passes down object values of 'animal'
}

function whatsGood (entity) {
     consol.log(entity,name, entity.emoji)
     <!-- ^ never said "let entity", we are ref the array - they are reference types - ref each other, but do not need to be concerned with the values dissolving -->

    animals.forEach(whatsGood)

    function hello() {
    console.log('sup')
    return 'sup'
 }
 function justDoIt(fn) {
    fn()
    fn()
    fn()
 }

 justDoIt(hello)
}

callback f(x)n can be anonymous when not given name -- also lamda f(x)n, or empty function 

filter
areas.forEach(area) => {
console.log(area)
animals.filter((animal) =>animal.currentArea == area) <--logs only who in each where
}

This will make more sense with practice

map creates copy of array with any transformations you apply
filter selects for particular info, so adding map on top of it within the selected filter provides an "updated" array
works as if within a subsection

*NOTE - copy js into console to see where it might be misunderstood
just llok at/copy in Mick's work for notes

function party() { 
    animals.forEach(animal => ){<-- for anonymous function only using one argument/parameter. you do not need 1st parens
    let randomIndex = Math.floor.Math.random() * areas.length<---Math.random is between 0 and 1, add area.length is between 0 and 4 Math.floor is round down - math.ceil would round up, but since arrays begin with 0, then we always use floor
    let newArea - areas[o] <---change 0 to randomIndex
    animals.currentArea = newArea}

    drawAnimals()
}

if you change data you need to update page = update DOM ()
so

function drawAnimals (){
    areas.forEach(area) => {
console.log(area)
animals.filter((animal) =>animal.currentArea == area) <--logs only who in each where
let inArea = animals.filter((animal) =>animal.currentArea == area)
let animalEmojis = inArea.map((animal) =>animal.cemoji + animal.name)
document.getElementById(area).innerText = animalEmojis.join (', s')
}

drawAnimals()

find - array method <-- array.find() one condition until found true for each elem in array

# Aug 16th *FIXME - Aug 16th Sam's lecture

Sammy's Sammies - checkout window w/cart
link all your fonts, mdi, bs, and own css
script tag src="" at bottom of body

pseudocode - write each baby step of the function action you want
ctrl + ` is open terminal

*NOTE - code small, test small
write pseudocode - very specific steps typed out in layman that WILL BE turned to code

computers as fast but dumb
write one function that does one thing really well

first thing is code console log - can the function be called at all? add the onclick()

*NOTE - onclick() can be added to any area, though technically ought to be only for buttons

let caprese = sandwiches.find() <--- word in parentheses is a filler, can be anything, related or not "banana word"
let caprese = sandwiches.find(sandwich => sandwich.name == 'caprese')

innerText targets within the existing HTML

innerHTML is actually writing HTML

duplicating to same id makes the console log stay, but the DOM not let two items be drawn to the same spot at the same time, though quantities will be tracked

forEach takes you into the index TO check for and access object level data

to read as string - use concatenation or string interpolation
template = `` <-- template is a banana word, but useful to say draw multiple sections w/o overwriting or copying every full line of code

(template += <---- add a new area (string line))

order is important here  --- remember JS runs top-down

*NOTE - anytime we have a 'placeholder' or 'total' that needs to be injected into from a *for loop* ---> we MUST declare and assign it OUTSIDE of the *loop*

single f(x)n multiple items (buy for each item is a single function, not each individual buy function per item)
^ ie - what you couldn't do yesterday

in HTML, pass a value in the universal onclick() so parameter a string onclick('')

find is a forEach under the hood

changing a set value? declare it outside the for loop BEFORE, then can += within loop condition

can use the .toString() method

= <-- reassigns value
== <-- makes comparison
=== <-- must be exactly this to be drawn or identified

string around interpolated values to pass down values to string literal

# Aug 17th *FIXME - Scrum lecture
Org structure - sort of // to the ideas around military division of authority, but with managerial trappings - OODA with corporate design

Sam doing game logic on new game based on Scrum - Zookeeper
Backlog -> In Progress -> Review -> Done
Sprints - task oriented progress of minimum viable product --> the real MVP

What makes it a game - what interactions? <-- backlog of tasks brainstormed (i.e. feeding, taking guest tickets, payment process, loss on animal death, etc...)

main>section.row in CSS will target the sections in main with row class

   # *NOTE - interval calls
setInterval( , ) <-- argument (set of instructions/callbackf(n)) and time (delay/"timeout" how often you want this to execute, time is guaged in miliseconds, so your number will be large)
^ functions as arguments are passed as set of instruction

setInterval(function) <--do not add function's () after, or else it will only invoke once, not set as an interval AS YOU PLACED THIS TO BE
^ setInterval(speedUpCoding(), 10000) <--bad
^ setInterval(speedUpCoding, 10000) <-- good
setInterval(() => {})

CLAMP - end limit to interval
i.e. IF hunger reaches 0, then redeclare object key to set #, in this case, keep it as 0

building duplicate lines? think about refactoring - ie, not making a feed button for each animal in a zoo
** create an update vs draw (changing preexisting vs new)


*NOTE - write "debugger" within a function - is a code to pause the code at that line when running in real time on the localhost8080

relate strings to objects to manipulate them --> puppeteer
alias all in array via full function, but based on specific onclick

function feedAnimal(animalName) {
   let founAnimal = aminals.find(animal => animal.name == animalName)
   foundAnimal.hunger ++
   if (foundAnimal.hunger>= 100)  foundAnimal.humger = 100

updateAnimal(foundAnimal)
}

now can write // function

function updateAnimal(animal) { <---name of object here does not matter, but it does in the functions within which it is called. Here is banana word, but it is a paramenter in the feedAnimal function
   console.log('updating')

   let animalStatsElem = document.getElementById(`${animal.name}Stats`)
                                                      //^consistent naming will be your friend
   animalStatsElem.innerText = `${animal.name} | ${animal.status} | ${animal.hunger}`
}

   # *NOTE - switch statement

Trigger a change in Y for change in X
consolidate based off of multiple conditions

   //#region
   //#endregion
   ^ to lock off and collapse code sections



# TBD Aug 18th

