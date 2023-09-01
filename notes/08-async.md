# Async - Mick's Monday wk 4 

check errors http.cats

when code runs it goes line by line, top to bottom
synchronous code goes to next line automatically
Asynchronous code allows for pauses in code
    ^ read or whatever, but wait...then continue

code has promises - will get info, start interaction, etc.
let prom = new Promise(() => {}) <---in console looks like: Promise {<pending>}
let prom = new Promise((resolve, reject) => {})
<resolve>: '' <--{<fulfilled>}
<rejected>: ''


without actually calling the parameters of resolve or reject, will never move past setTimeout

try{ <-- errors here are hit and the code stops running and jumps to the catch, allows "type of forking" so that certain code runs despite an error occuring in one place. lets you code down a different path because you won't be running bad code

} catch(error) { <-- errors in here are run and run past

}

*NOTE - Promises create functions to pause standard synchronous running of code
if you do not have any AWAIT portion in function. then there is nothing async to run - can only AWAIT a PROMISE
^the retun type of Pop.confirm is a promise <--which is boolean
if you put AWAIT, nect line is not read until a confirm or cancel button is pressed - you are logging a resolution
^ if you see PROMISE in your console log, you did not use AWAIT

Promise is a class of its own
^ other applications can give promises, and that is where we will work, ie - POP

API - application program interface
APIs are not databases, the app interfaces with other apps - lets them talk to a database, but not limited to database

    #SECTION - Getting monsters based off of Zelda API

fetch() <-- promise w/ a response in it
      ^ request info or url
      can get API
async getMonsters{   
const response = await fetch(url)
}

Dev tools NETWORK tab
change from ALL to FETCH/XHR
preview will give you a code- oriented readable bit


*LINK - script tag axios



# REVIEW Sam's Tuesday Aug. 29th lecture -- Gregslist with APIs and async
CRUD - Create Read Update & Delete


*NOTE fake sign in info:

quibbles@gmail.com
6regsListASYNC

MAKE SURE 3RD PARTY COOKIES ARE ACCEPTED SO AUTH0 RUNS


  #  SECTION - Gregslist API
bcw create
MVC-AUTH <-- must log into app
gregslistASYNC

  #  SECTION - Set-up, building out project
Do NOT start w/ model --> we are taking external data, so we need to know their terms to make our constructor

sandbox.codeworksacademy.com
    Look at the models

Create:
CarsController
    Export class
        constructor
            console.log check
CarsService
    class
        export const carsService = new CarsService()

Router
    test carsController

    set new path
        #/cars
            controller: CarsController (return homeController to first)
                view: 'test string'
index.html  <---add "a tag" to get to view
    <a href id=cars>


*NOTE - can get rid of about page

return to controller
Goal: when you go to cars page, you want cars API to show cars
^ constructors run immediately so ...

CarsController method

async getCars(){
    try {
await carsService.getCars()
    } catch(error){
        Pop.error(error.message)
    }
}

NOW GO TO SERVICE to create method in Service
const _sandboxApi = axios.create({
    baseURL: "url", <--often append with the relevent endpoint for page *elsewhere*
    timeout: 8000
})


async getCars(){
    <!-- throw new Error("Method not implemented.") -->
    const response = await _sandboxApi.get('api/cars') <---- here is where we "finish" the URL so that the specific endpoint is reached
log(response.data)

}
^^ when using axios your response will always be wrapped in "data"
dev tools
    Network
        Fetch/XHR


NOW we know what data will look like, we can make model

MODEL
    export class Car {
        constructor(data){
            IN DEV TOOLS, RIGHT CLICK ON ARROW OF THE FIRST OBJECT IN ARRAY AND COPY IN model (underscore ID or reg will work)
        }
    }
^^whole object will show in with object having subproperties (this.creator in codeowrks sandbox)
can do this.creatorID = data.creator.id
        ^this is 'flattening out a data object'
        we are 'adapting' the data object properties into our own property in our class


        async getCars(){
    const response = await _sandboxApi.get('api/cars') 
log(response.data)

const mappedCars = response.data.map(dataObj => new Car(dataObj)) <--passing data from API through cars constructor
log('mapped cars', mappedCars)

}


APPSTATE
under/within class

/** @type {import('./models/Cars.js'.Car[])} */ <---this is just industry standard helpful
    cars = []


back to Service:

        async getCars(){
    const response = await _sandboxApi.get('api/cars') 
log(response.data)

const mappedCars = response.data.map(dataObj => new Car(dataObj)) <--passing data from API through cars constructor
log('mapped cars', mappedCars)
AppState.cars = mappedCars
}

back to Controller

universal function
function _drawCars(){

}


CarsController method

constructor(){
    this.getCars(
        AppState.on('cars'_drawCars)
    )
}

Router:
comment out view --> now model in HTML the template you want
section out what is going where
copy, comment out, put in MODEL

MODEL
    get cardTemplate(){
        return  `
        *formating from HTML* <-- with string interpolation
        `
    }


Controller

function _drawCars(){

    let template =``
    AppState.cars.forEach(car => template += car.cardTemplate)
    setHTML('cars', template)
}
*NOTE - axios service is a script tag for HTML

  #  SECTION - Creating new data - form

  getbootstrap.com <--find a model for collapsable button

  *NOTE - be sure to add a row for the button in HTML
  ^refresh, see how it looks, then add your own info
 1. There is a toggle component with an ID target
 2. There is a div with the appropriate ID

 *TODO - *copy form from first gregslist!!!*
 ^ be sure to change properties to align with the API
  #  SECTION - Create new data controller

 createCar(){
    window.event.preventDefault()
    const form = window.event.target    <---targets onsubmit
    const formData = getFormData(form)  <---creates the object from the form <--adds car to API
    carsService.createCar(formData)    <---gotta await service, SO
    log('create')
  }

SO:

  async createCar(){
    try{
window.event.preventDefault()
    const form = window.event.target    <---targets onsubmit
    const formData = getFormData(form)  <---creates the object from the form <--adds car to API
   await carsService.createCar(formData)    <---gotta await service, SO
    } catch (error){
        Pop.error(error.message)
    }
  }

  #  SECTION - create in service

async createCar(formData){    <--POST request = must supply some kind of body<--'body' is what we are trying to insert to  (post is an HTTP)
const res = await _sandboxApi.post('api/cars', formData)    <--adding info to API, will likely need to also get to local AppState
log(res.data,'we are creating a listing')
}

401 error -- unauthorized

database and API can talk, which means whoever can access API can access your database
SO
use 3rd party provider so people cannot dir access API
domain, audience, and clientId from sandbox needed

  #  SECTION - env.js
  env.js - environment

  copy over info from sandbox
  ^connects to Auth0, we still need to log in.

  AXIOS service - baseURL <--imported from env.js
  in ACCOUNT service - the endpoint is imported from AXIOS

  carsService has baseURL SO:
  change env.js baseURL and put it as the base, which will now be auto imported into AXIOS service


  in service
  await api.post

  async createCar(formData){                ⬇️ body/payload
const res = await api.post('api/cars', formData)    <--just await api, now
log(res.data,'we are creating a listing')

const newCar = new Car(res.data)    <-- already formatted data, mapped back into constructor, hence not using formData
AppState.cars.push(newCar)
AppState.emit('cars')
}
  #  SECTION - changing pre-existing data
can we redo form to allow for editing? Yes.

  async createCar(){
    try{
window.event.preventDefault()
    const form = window.event.target    <---targets onsubmit
    const formData = getFormData(form)  <---creates the object from the form <--adds car to API
   await carsService.createCar(formData)    <---gotta await service, SO

   form.rest()
   bootstrap.Collapse.getOrCreateInstance('#carFormCollapse').hide() <---hiding drop form
    } catch (error){
        Pop.error(error.message)
    }
  }


  need a model to edit, so
  CANNOT have it HARD-CODED in HTML

  MODEL
    static CreateCarForm(){ <---static is similar to getter
        return `form template`
    }


change HTML
change Controller
drawCarForm(){
    <!-- new button app.Controller in onsubmit <--id for draw location stays active on HTMl -->
setHTML('carFormCollapse', Car.CreateCarForm)   <--look at Sam's notes in the controller
                <!-- access ^ similar to getter, but STATICS exist as members of a CLASS(the ting you are exporting), vs PROPERTIES of an instance(the things within a class) -->
                <!-- NOT new Car().CreateCarForm() <--- that is for getter-->
}


AppState holds instances of a class
  #  SECTION - Back in MODEL

get ComputeEditButton(){
    if(AppState.account.id == this.creatorId)
    return`
    *edit button*
    `
}
^AppState account is holding your creator ID

get ComputeEditButton(){
    if(!AppState.account) return ``   <---same as (AppState.account == null), so return empty string
    if(AppState.account.id == this.creatorId)
    return`
    *edit button*
    `
}


get ComputeEditButton(){
    if(AppState.account == null || AppState.account.id !=this.creatorId) return ``   <---same as (AppState.account == null), so return empty string
    <!-- if(AppState.account.id == this.creatorId) -->
    return`
    *edit button*
    `
}


In CONTROLLER add listener to constructor
AppState.on('account', _drawCars)


setActive(carId){
    <!-- add as onclick to ComputeEditButton in MODEL -->
    log to check and see if it works
    log('edit car', carId)
    <!-- got to target by ID -->
<!-- set the chosen car as active -->

carsService.setActive
}

in Service

setACtive(carId){
    let car = AppState.cars.find
    AppState.activeCar = car
}

in AppState add activeCar = null
  #  SECTION - Now can draw edit form
CONTROLLER

  function _drawEditForm(){
let active = AppState.activeCar
setHTML('carFormCollapse
, active.EditCarForm)
}
ADD listener to constructor
AppState.on('activeCar'_setActive)



in MODEL

copy static form

and set as

get EditCarForm

add value"" for each via string interpolation

in appstate Car||null



  #  SECTION - Up the specificity so new info is saved to API correctly

  changes in EditCarForm to differentiate from create car layout


  in CONTROLLER
  try-catch

  editCar(){
    try{

    } catch(error){
        Poperror(error.message)
    }
  }

  ^ will look similar to create car method

 async editCar(){       <-- edits will lokk similar to creates
    try{
        window.event.preventDefault()
        const form = window.event.target
        const formData = getFormData(form)
        
        carsService.editCar(form)


form.reset()

bootstrap.Collapse.getOrCreateInstance('#carFormCollapse').hide()
    } catch(error){
        Poperror(error.message)
    }
  }

  in CONTROLLER

 async editCar(formData, carId){
    <!-- throw new Error("Method not implemented") -->
    <!-- put request, change overrides base API info api.put -->
const res = await api.put( `api/cars/${this.id}`,formData
log(res.data, 'editing car'))

const updatedCar = new Car(res.data)    <--alias so as to slice: to remove and replace

let oldCarIndex =  AppState.cars.findIndex(car => car.id == carId)

AppState.cars.splice(originalCarIndex, 1, updatedCar)   <-- 3 arguments: what to take out, how many of what to take out, what to replace it with

AppState.emit('cars') <-- emit to trigger the draw after the splice
  }

 *NOTE -  ^^ splice will remove any number of index from an array based off of the starting index. Last optional argument is what we want to replace <-- without argument 3, you simply delete
 ^ the last argument will always replace the first or given index
 ^splice gives immediate reactivity

  pass down ID in the model's CarEdit

  in the drawEditForm
  bootstrap.


  getting 404 error --> not found (not enough info to ID correct car)
  ^ issue in request URL under Headers in the Fetch/XHR of Network in dev tools


#   SECTION - DELETING

new compute in model

get ComputeDeleteButton(){
    iff(AppState.account == null||AppState.account.id != this.creatorId) return ``

    return  `<button onclick=app.CarsController.deleteCar(${this.id})>Delete Car</button>
    `
}

in CONTROLLER

async deleteCar(){  <--must add button to cars template
    try{
        if (await Pop.confirm('confirm?')) {
            carsService.deleteCar(carId)
        }
    } catch(error){
        Pop.error(error.message)
    }
}
    const res = AppState.cars.


    in SERVICE

    async deleteCar(carId){
        const res = await. api.delete('api/cars/${carId}')  <-- check this against Sam's work, I thnk this is right
        const filteredArray - AppState.cars.filter(car => car.id != carId)

        AppState.cars = filteredArray
        AppState.emit('cars')   <-- optional, can delete
    }

   # *SECTION - CarsView

   Take template from router to own cars view - so you can make multiple pages

   AFTER env.js, remove from HTML for auth information, haha
   should not need to touch the env file since changes were made already by Sam


# *REVIEW - Sam's fireside debug sesh

*SECTION - MAKING ISSUES

error checking

404 not found - check env.js
check service - make sure file path of imports is correct


be sure the view page IS exported


make sure CLASS attributess are not mixed in with ID ones --> draw won't be correct

make sure HTML and router directions are matching


in CONTROLLER check constructor to see -- based on APPSTATE if listeners are titled the same

SERVICES needs async and await in functions for draw <---// passing drills, gotta wait beofre advancing


NETWORK tab MUST be open when testing things, or will not catch error for you to see

path//property - make sure your keys align with the form data
^ make sure names match on each aspect of the form to ensure proper path

*SECTION - EDITING ISSUES
make sure info is aliased or has full route to hit edits

check for all the "s", whatever comes before the issue is undefined, hence the next bit cannot read
MODEL is singular, ALL else is plural

404 error - cannot identify correct path <--make sure url will read like a web page with all the correct slashes

is there a PAYLOAD tab? is the SERVICE need to pass both arguments that include the logged changes

*SECTION - DELETING ISSUES

CONTROLLER - make sure all ASYNC has AWAIT within the function

# REVIEW Mick's Aug. 30th Wed. lecture DnD API

SANDBOXING so must create via MVC-AUTH in the COMMAND PROMPT

SCSS variables --> what the bootstrap css is based off of
^if you change, you must recompile the styles:
In TERMINAL:
NPM RUN SASS

(Syntactically Awesome Style Sheets)    <-- not a joke

set AXIOS- use the base URL and timeout
put AXIOS into SERVICE 

*NOTE - SLOW DOWN WHEN YOU CODE AND CONSOLE LOG EVERYTHING

*NOTE - we went axios, service, controller

console.log(Object.keys(obj).join)

all DRAWS go to CONSTRUCTOR for sure w/ LISTENER

   # SECTION - static template

spell list template that is static
part of the definition of a class, not an instance of a class

? in CONSTRUCTOR of MODEL "is there this..or is there this" if there is a, return this, if there is b, return this, if there is neither, return this

use STICKY-TOP to get card of selected item to appear as you select it.

   # SECTION - getting things to your own list
   for new data models or APIs, make new C/S for each

   create new CONTROLLER and SERVICE just to talk to sandbox

   user or account as first parameter for listener on getting own list

   MAP creates a transformed copy of the array

   you CANNOT send classes over the internet, hence the transfiguring into local storage once data is received


# #REVIEW - Sam's Aug 31st NASA API lecture
api.nasa.gov

formatting queries <-- always start with a question mark, followed by parameters
                          ⬇️⬇️            ⬇️new param ⬇️
api.nasa.goc/planetary/apod?api_key=DEMO_KEY&date=___________
   # SECTION - Creating project
   *NOTE - Sam used the style sheets, look at the work there, too

check API data and compare to SANDBOX

make new SERVICE
make new CONTROLLER, log
replace controller in ROUTER
^ should see CONTROLLER show up

write a TRY CATCH in controller to GET API <-- will be ASYNC
in SERVICE before CLASS make AXIOS instance <-- base URL and timeout
    write // GET API
also
    PARAMS in AXIOS instance
 {   'api_key':}    <--can have multiple parameters, separated by commas {'api_key':____, 'date':____}  < these are specific param keys to NASA

 once you can get that arranged AND see ALL the object info in the CONSOLE

 go create MODEL <--BASED ON the SANDBOX arrangement of data

 this.x = what we call it
 data.x = what it is in API
                        first choice || second choice

want to save, so go to APPSTATE
@type {import{`./models/Apod/js`}.Apod| null}
activeAPOD = null

back to SERVICE
in ASYNC GET 
AppState.activeApod = new Apod(res.data)
log!

should see API *and* SERVICE in page CONSOLE, so log BOTH

in CONTROLLER ⬇️ this is what it is called in APPSTATE
AppState.on('______',_____)
                      ⬆️ is the function to call


draw f(x)n in CONTROLLER, include url for background image in string interpolation


go to env.js --->move in Auth0 sandbox info
⬆️ this is to SANDBOX aka OUR data

min-height will adjust and be reactive in ways height will not, only images will be static height

# SECTION - DATE PICKER       <!--    ⬇️ boolean when upon selecting a value the new value input then changes the data-->
hook up date box from input to an onchange to get APOD by date INPUT tags are clickable

ASYNC getApodByDate(
    try {
log!    <----string in to see if you can get a response with any date picked
    }
    catch(){

    }
)
change to:

    try {
log!
const input = document.getElemById()
const newValue = input.value
log(newValue)
    }
    catch(){

    }
in SERVICE
make // ASYNC that *pulls from* API
⬆️ MUST  throw new data through model

   # SECTION - sandbox time
gen SANDBOX service and controller

hook up onclick to CONTROLLER

in SERVICE this will have a POST from the API

log so that you can see what info is getting passed into the sandbox

BS offcanvas
works similar to COLLAPSE
^ can copy from bootstrap, but will need to change things for your design

in DRAW
needs to ref APPSTATE
and FOREACH gen a template <-- from MODEL *to* HTML section (by id)

gotta pass any new info through constructor in the PUSH
have to EMIT from APPSTATE before it will be triggered by CONTROLLER draw


interpolating sources is tricky - 404 errors probably originating in the templates in MODEL

   # SECTION - need get request

async a try-catch in SANDBOX CONTROLLER <-- throw into constructor so they load with page
to get favourites via SANDBOX SERVICE <--GET from API('endpoint after sandbox's base URL')
*NOTE - if you fire off request before account is registered, it will log a 401 error in spite of you being logged in.
^add a listener in the CONTROLLER to make sure the account is loaded BEFORE drawing this.favourites

be sure stuff in SANDBOX SERVICE is getting put into the APPSTATE
^need to MAP data
            place it throw constructor
                    plug new value into APPSTATE

   # SECTION - deleting

in MODEL
    add and place button with onclick option to delete buttons can have titles which display on hover
                                ⬆️ will be linked to SANDBOX CONTROLLER methods
                ^ be sure to emit, BUT
                                    in order for it to be visually removed at the time, must FIRST run a fildered array where that specific ID is not longer supplied
                                    THEN can delete the EMIT line altogether, as the filtered array is being sent


   # SECTION - re-draw favourties to background

ADD onclick to favourties template in MODEL
        can use existing getApodByDate from NASA CONTROLLER (*not* the SANDBOX one)
            pass and argument as string('${this.date}')

                    Must now extend out NASA CONTROLLER with argument, BUT
                            *still needs to work with onclick*
                                so cannot be the parameter in the await portion
                                    write an IF
                                            if(date){
                                                await nservice.getapodbydate(date)
                                            }
                                                rest of original function
                                                await nservice.getapodbydate(dateValue) <--other aliased constant that exists

                                        


   # SECTION - checkpoint relevant stretch goal: toggling element visibility

   button on page to look for all the elements on page and toggle visibility
   BOOLEAN - T/F
        In APPSTATE
                isVisible = true
                    ⬆️ this defaults false so that you CANNOT see the elements

                    ID all that you want to hide    <--these do not need to be named the same
                in NASA CONTROLLER
                        add universal function
                            grab all elements by Id via let xElem = document.getElementById('')
                                all button will do is flip BOOL in APPSTATE
                                    link to NASA CONTROLLER
                                        toggleDisplay(){
                                            service()
                                        }
                                            in SERVICE
                                                log
                                                appState.isVisible = !AppState.isVisisble <--- will change true false with each clock
                                                EMIT
                                                    add LISTENER in CONSTRUCTOR
                                                                put all drawn Id tags into an array
                                                                if(appstate.isVisible ==false)
                                                               { elems.forEach(elem =>elem.style.visibility == 'hidden')}
                                                               else {
                                                                elems.forEach(elem =>elem.style.visibility == 'visible')
                                                               }
# *REVIEW - Jake's Thursday fireside lecture: Pokedex
*STUB - Jake was being lazy due to time restraints

Roll up the proper controller in the router

Ctrl + click on a handler will take you to the tab, or Ctrl+p will let you menu work it

Ctrl + . to type and place line in new file --> even if it does not exist, it will write one

    #SECTION - in service
*NOTE - In checkpoint, will only need SANDBOX api!!!!!

put additional APIs into the AXIOS
^ will also log for error handlers if you copy the existiong ones and align the API name

console.log the res after you async await the API in the service
console.log(res.data) <-- see what you are dealing with

aysnc the get with a TRY CATCH

you want an instance of a class, so SERVICE export is different, not whole class, hence at the bottom

NEED BEARER TOKEN - get passed the unauthorized in sandbox


async getMyPokemons(){
    const res = await api.get('/api/pokemon')
}

test in constructor401 - is trying to run before account is accessed!!!!!!!!!
The network tried to get stuff before auth info was confirmed <---need to make a listener in APPSTATE
    run AppState.on('account', this.getMyPokemon)   <-- no () or else you invoke immediately we do not want f(x)n to execute, just use as reference or else the PEMDAS rule applies

Controller will need set-up where the auth runs first, or else other things WILL always break

all the APPSTATE links can then be used to add buttons and functionality in SERVICE in the getPokemons f(x)n


*NOTE - make sure CONTROLLER's draw functions are in CONSTRUCTOR with listeners set after the API has been reached, or else will not run.
*ie, the order of AppStae.on() is important*
API's will ban you if you trigger looped draws in you listener

async getPokemons(url = '/pokemon') <--or statement
ternary in the go method


if you Ctrl + . in CONTROLLER before the command is in SERVICE, will create a dummy version there for you to swap out details