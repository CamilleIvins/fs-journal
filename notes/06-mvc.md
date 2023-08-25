# MVC

# Mick's lecture Aug. 21 - design patterns

check figma - https://www.figma.com/file/g5YmEFVGKAF2BWUqQJ3ng6/MVCS-Diagram?node-id=0%3A1&t=BB2R4cKdv1A60Oth-0
has service and state centers for process

![MVC diagram](image.png) <--added to notes section

View and controller are dir interacting, but behind view is a series of info boxes related to the actions that go into the controller
Controller as segue to business logic which is stored in the service sector

appstate holds stable code - such as arrays

bcw create <---- will be the code used in command prompt from now on -- faster than touch
download frameworks that come with own template - like react or vue

we are doing mvc today


can do git init  Y/N <--will push to personal github, so be careful about this if you have multiple you operate
 CANNOT do "code .", but enter into as prompted
 still one linked file to HTML, but only main "controller"
 main.csss is the bootstrap

 package json  -- dependencies - copy internet code into own, node modules <-- important in two weeks (bootstrap and sass)
 bypasses cdn link that is not active until loaded, comms directly to the program

 class Character {}  <-- cap Character because it is a ref to definitions
 ^ all keys are empty, is a blueprint, not object is entered, just what values they will hold per character

 classes create blueprint for onject data

 so let Ent = new Character <-- get new character -- adds object to character array
 w/in class, set 
 constructor(data key, data key2, data key....){  <----temp vara as parameters for the scope of this function, do not actually link to the Character keys *themselves*
    ^ this provides for each time you build new Character
    <!-- where do yuo put these materials -->
this.dataKey = newKey
this.dataKey2 = newKey2
this.dataKey... = newKey...
 }
<!-- *NOTE - this is a context for a class instance to look at itself -->
this. <---object looking at self
instance member -- properties, members are whatever exist on class


can add functions w/in now that can ref these keys for each character ie - can ref themselves, multiple chars cannot ref each other (with this setting) you have context of self only

   # SECTION - AppState JS

    Focus mainly, today, on class OvservalbeAppState extends EventEmitter{
place to sroe all of data
create arrays
Characters[
    new Character <----orange icon option *these will nt work without ref to other page WHERE CHARACTER WAS ACTUALLY DEFINED
    ^ must import, only works if it has been exported
]

        <!-- right now, even ignore page=`` -->
    }

# *NOTE - how to import - type out what you want to import and it will finish, but do not type out whole, as typos in import statement are hard to find

    SO export class Character{}

    top of page, type "Character" and press tab, will auto gen, but SINCE FILE IS OPEN IN OTHER TAB only when open in other tab, can auto generate the import line

    xCode, jetbrain, and vs code as major industry players

    AppState data is not accessible within console = you cannot pour lighter fluid into engine while driving

    within init() can throw things into console

   # SECTION - create new controller
 this js file will be wholly exported to everything else
 write the entire file withong a controller class

 export class CharactersController() {
constructor(){
    console.log('this log will not show on page')
}

 }

*ANCHOR - app.js is what is pulled into HTML
SO within this app.js is a router, essentially
router.js has a path, controller, and view <--what gets loaded into page

can change objects w/in an array that is a const - can change data within, but not the structure around it

w/in 
 export class CharactersController() {


constructor(){
    console.log('this log will not show on page')
    this.drawCharacters()
}

drawCharacters(){
<!-- AppState.characters <--will open dropdown of options -->

let content = ``

AppState.characters.forEach(character => content += character.name)
document.getElementById('characters').innerHTML = content
                            ^this does not exist on HTML, but does on router
}

 }

parseInt => turns string to number by pulling internal number from prompt

window.prompt vs alert ==> can enter info

*NOTE - functions in controller only responsible for taking in actions and does NOT perform data manipuation (business logic)
   # SECTION - services

class CharactersService() {

yourFunction(para1, para2){
    same info from controller
    console.log to see if you passed the values from one js file to another
}

}
wxport const characterService = new CharacterService()


app only knows controller, system does not deal with anything else -- still all front end

throw characterService. into characterController

load order of imports is important if one refers to another

use "get" similar to function, but goes without parameters, runs as a property with value ONCE you access it


*REVIEW - in general, start with model - what does the data look like, what do you need to support within app

stick some of those in AppState

create controller, have controller draw data (either html or string concatenate)

add interactions to page elements

the rest...



# Mick's Aug. 22 Tuesday lecture

generate export class in new models
w/in constructor you can gen properties of new array

page load --> router looks at the broswers URL and matches it with a PATH, then loads the corresonding CONTROLLERS and injects the VIEW  into the index.html #router-view

in controller, draw function via AppState <-- draw to constructor
add template w/ empty string -->for each draw template (throw into router, so show on page)
get elem by id ==> draw to html page

setHTML('id', templateName)


switch(this.rarity){
    case='rare': return 'class of rarity style, more than one class'
    case='ultra-rare': return 'class of rarity style'
    default: return 'common'
}

interpolating a string removes the quotes, so add them back in in order to generate a data point for a specific player only for STRINGS, ie, names

create as service (export the service so no one can deal w/ this on user end)
^instance vs definition, so no one can redefine it (can't nerf via the console, makes service unavailable to user)

can let code know you are setting an array by typing above
   #  *NOTE - <!-- @type {array OR array object name} below the array, so that it is always read as array in other js files importing it--> use /** */
code will still work, but will throw questions/errors during coding as VS code will try to treat it as a string

   # SECTION - listeners/observers

The constructors job is to create 'listeners' for changes in the AppState
AppState.on('looks for changes in this method', fires these instructions no parentheses)

   # SECTION - buy style
changes router view based off of id "router-view" placement

onclick="app.playersController.buy()" role="button"

move into service js
"CTRL + ." <--create method in your service you are referencing from another file

in AppState

@type {players[]}
allPlayers = []

SO

draw in controller

in service

const allPlayers = appState.allPlayer
let playersContent = ``
allPlayers.forEach(p => playersContent += p.originalPlayerTemplate)
setHTML('allPlayers', playerContent)
AppState.allPlayers.push("newPlayer <--what I need it to be, but not what synched with Mick's lecture")

add HTML to draw to row

in controller
AppState.on()


problem - change in one object can change in another, since data keys are changing, not objects

two ways to trigger change in arrays
1. totally reset value <-- does not log last rendered value w/o all random and all with syntax operator called spread to pull info out of array, then put into new array
...AppState.array-1, array-2

2. AppState.emit("arrayName") <-- can be put in any of the js to be triggered
so use PUSH, then EMIT method


listeners are regitered to appstate keys <-- triggered when values change

   # SECTION - save data

local storage
 UTILS --> store.js

 in service, write a save f(x)n
 saveAllPlayers{
    saveState('bananaWord', AppState.allPlayers)
 }

 Throw this into end of function that will uopdate data

 in AppState
 UNDER INIT{}
 loadState('sameSaveBananaWord', [players]) <-- referencing the model

 to use local storage must make classes using data objects, NOT flat objects


 START WITH DATA OBJECTS

 # - Sam's Wed Aug 23 lecture

 Design is very related to the afternoon assignment
 creating a Craigslist-esque site

 bcw create

 generate constructors to build instances of a class
 loading data from local stroage and passing through the array of original class <--problem as parsed back into object, so a solution is to wrap in curly brackets and pass it as an object w/ properites

 SOLUTION
constructors cannot have multiple properties
 constructor(data){
    this.name = data.name <--- just look at what Sam did
 }

is BETTER than

 constructor({name, price}){
    this.name = name
    this.price = price
    this.description = data.description
    this.listingDate = new Date()
 }


 MDN date

 in AppState - gen dummy data (instances for model page)

 Type UNDER page=`` AND @type

 cars =[
    new Car({
        make: "BMW",
        model: "335i",
        year: "1973",
        price: 
        isNew: 
    })
 ]

   # SECTION - cars controller

export class CarsController{
    constructor(){
        console.log('testing, testing CarsController')
    }
}

put new section in ROUTER to create a cars-specific page
path: "#/cars"

private function is placed above the export class in the controller

w/in class = member
outside class =/= member
underline before name of function is best practice - visual indicator of private class
^ why make private --> background processes, do I need to call outside of when this is run again? interface, what user sees

functions are own thing, methods are members of a class, can run in background as updates happen, not dependent on membership, keeps hidden from users

alias out data from AppState to iterate through list and gen HTML that will be drawn to page

elevation class raises as card above background

   # SECTION - Forms

go to get bootstrap and use preset layouts and copy to page
forms are take and fill with the data type that will be taken in to filter data

most every form attribute must have 'required', so as to make them fulfilled before submitted
can also specify patterns
   #    SECTION - form is made, now make it do things

   use of id tags to make


   app has access to controller, but renders from service  (which takes from models) which cal manipulate AppState

   est inputs so that when form is submitted the values can be grabbed <-- taken based off of name input with value sub-assigned
   # SECTION - creating the car service

class CarsService {

}

export const carsService = new CarsService()

must alias out data through form data controller so that it is recognized as a car

controller handles all user submission, so deal with data at this level before it reaches service layer

put a listener in controller for the appstate to update; push is an array method, so
1. reasign value in appstate ---> yuck
2. AppState.emit('cars')
   # SECTION - local storage

in service write a save utility OUTSIDE class
argument is the key along with AppState item ('cars', AppState.cars)

must set a loadState in the controller
cars = loadState('cars', [Car])

generate id must persist off of reloada, so pipe operate it to allow default data, so data.id
   # SECTION - delete a car
 in controller after html-ing a place for it
 create method
 set listener for car service

 in service
 app.CarsController.deleteCar('${this.id}')
 console.log('deleting', carId)
 AppState.cars (entering Service layer)
 let foundCar = AppState.cars.find(car => car.id == carId) <------
 AppState.cars AppState.cars.filter(car => car.id != carId) <------- filters out car we want


 in service IN class

 both create and delete

#  Aug 24 Mick's lecture
 Scrum sprints are 1-4hrs
 daily catch-up --> what did you do yesterday, what will you do today, and what obstacles are you facing?
 Rterospectives plot for changes to next sprint

 designers are the worst testers, you won't break it on purpose, so user testing is most enlightening --> think like escape rooms

#  Aug 24 Sam's lecture - Redacted: Flow, set-up, and tasks
getting redaction to happen on a document

   # SECTION - setup
generate constructor in MODEL

build dummy cases in APPSTATE

got to CONTROLLER --> build constructor and console.log() confirm constructor is present
gen all data you will log

LAST to generate is the SERVICES page, even if you are not ready to write business logic
for starters, simply set up and export const class

   # SECTION - first draw

private draw function in CONTROLLER (above export class)
invoke in the constructor below

build what we want drawn in HTML for ease
container-fluid
row
col |   col

*NOTE - it helps to have an idea of what you want the page to look like in the end when you draft templates

put template in MODEL with GET, uses RETURN `` command

get data from APPSTATE
create 'blank' template ''
iterate FOREACH and add template to each case


pair SERVICE and CONTROLLER and log to check if info from MODEL are being tagged in
then in SERVICES
generate var via APPSTATE.object.find()

NULL allows to read object as true or false, so a na active case will either be null, or have the selected case
^sets a default


for active cases, put listener in CONTROLLER for the active case in APPSTATE
^listeners req 2 parameters, ('string of title', _drawactive) console it out to test

create new template for active case, which will take a card from the array and open it up --> so new template despite having general one.
^separate displays allows for minutw changes, like difference in buttons once accessed

   # SECTION - redacting info within a string
getters re-run every time we instance it, runs loops, so can add a ton of stuff BUT this slows process as getters get bulky

*NOTE - all data manipulation happens in service
controller just handles input, but all true changes are in service layer

   # SECTION - saving and editing info
 deal with setting and resetting active view so as to lock and unlock.
 BUT
 saves are not yet saving across page resets. Need local storage

   # SECTION - local storage save
in SERVICES create a save function with an internal argument of saveState <--built in
can invoke in arg w/in class to save to local storage

BUT not loaded up

hard coded data is still being drawn.

SO

loadState

if you can save before load, they get saved and the hard coded cases can be commented out!

MDN, bootstrap select - for dropdown select list

with local storage up - we can now move to open new objects

   # SECTION - creating new objects
everything will need to go through SERVICES page for making or altering form data
created in CONTROLLER, still is manipulating data

DUE to SLICE must fill in dummy string via || so as to not draw errors

   # SECTION - async

   all ASYNC functions must have AWAIT
   MUST wait for users to respondinAPPSTATE do not leave dummy array and loadstate --> loads top down, and will mask any new inputs/creates


