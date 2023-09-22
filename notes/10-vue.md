# Vue - two wweks of this, look in wk 7 folder for lecture that week
Vue created by Evan You (Chinese Singaporean)

Vue, Angular, and React do the same thing, but the key is styling. They are ALL Javascript at their core, diff mainly in syntax
Do what you enjoy and what you find easiest.
    junior devs use what your senior tells you to
        this week - try only Vue
            next and after, try to recreate old checkpoints in all three

# Jake's Monday, Sept. 11th, Vue lecture
bcw-create
    vue-starter (scroll down to find)
        src file - plug in env.js info
            start server --> no longer bcw-serve, does more, is the Vue program of hosting (vite)
                Hot module reloading - reloads only the updated code
                    will refresh if backed up, or will req manual refresh if you do something and it is not reactive
    TURN OFF AUTOSAVE
        The reloads will be chaotic
#    #SECTION - file tour
editor config
package.json - keeps track of dependencies
    check the versions, you may need to update numbers
vit.congfig.js
*SECTION - src
NO controllers
    pages, models, services same
app.vue and main.js
    main.js is entry into your application - loads app.vue and router.js
registerGlobalComponents.js - this is the code to go to components that --> the // to CONTROLLERS
    Component is both CONTROLLER and VIEW combined
        this is love or hate - single file components have sections for each type within the file (js, css, html)
            Login component is single component, if you need it elsewhere...you need to rebuild it elsewhere
    OOP         abstraction, encapsulation, inheritance, and polymorphism
                      ⬆️ and ⬆️ are going to happen everywhere in order for components to work sanely
                        otherwise too much code
                            these frameworks were written with the OOP pillars in mind
JS is mixed directly into VIEWS, like with view models in MVC, but this is...more intelligent, and have different syntax

*NOTE - "v-"
v-  <-- this is important, and used in both Vue and Angular
v-bind: --> is shorted to "@" when bound to an EVENT, some will be ":"
{{}}    <-- binds // to the ${this.x}

if a router link is broken, will not render, throws error

#FIXME - if # of code lines > 150 lines of code <-- too much in one file, or poor code
if you are >180 lines, Jake will force an error thrown
very often, 120 lines is the MAX

all script changes will require changes in template above
NO draw functions - default in Vue

components witten have to be used in order to show up

in Navbar.vue <-- login component is placed

components will ref each other, can have near infinite nesting with good abstraction

#   #SECTION - need to install vs code extention to do styling and script in same template page

#   #SECTION - App.vue
header and footer are in here

Pages folder has all the smaller views
recursive components will try to continually draw, so be careful
    ie, don't put navebar in the navbar vue page
        MAX call stack size exceeded error in console

Keep dev tools open - Vue errors are different
    capitalization is essential
        will not render (draw) if the name is not a perfect match

        Hot module reload something went wrong = need to manual reload
  *LINK -         if white page = Vue will not render an error - often OFTEN a ROUTER LINK error


main.js is a huge import page
*NOTE - #   <-- "#" is the ID key in CSS

single "outline" component will be put on loop as content is updated


# - install Vue dev tools for browser, vs code extentions to run components
https://devtools.vuejs.org/guide/installation.html
only shows up in browser tool with color when Vue was used to dev the page
options for angular and react
ie
    Angular Language Service, and typescript extention

*NOTE - extentions will conflict with one another, so be careful
AND
*NOTE -     DISABLE unused tools for workspace you are currently using
ie do not keep react open with angular and vue
SAME  with C# and BOOSTSTRAP

Sam slacks snippet for Vue template

# - Jake's build

#   #SECTION - reactivity
homepage is in pages

we can put stuff to page, but we NEED data to back our numbers
     this is placed in script   <-- the CONTROLLER section of our view

    export default {
     setup(){
     let health = 100
     return{
        health,
        attack(){
            health --
        }
            }
         }
    }

import {ref} from 'vue'

    export default {
     setup(){
     let health = ref(100)
     return{
        health,
        attack(){
            health.value --     <-- now object with .value property, is proxy object
            console.log('HEALTH:', health.value)    <-- .value is always unwrapped by default
        }
            }
         }
    }

This is not in APPSTATE, though. DATA should not live outside appstate

 export default {
     setup(){
     
     return{
       
        attack(){
            
        }
            }
         }
    }

    Property "" was accessed during render but is not defined on instance = values are not in JS

#   - APPSTATE
do NOT change data in controller
    that is for SERVICE
import {reactive} from 'vue'

*NOTE - only objects can be reactive
    can be subscribed to

in APPSTATE 
health = 100

import {computed} from 'vue'
import {AppState} from '.../AppState.js'
 export default {
     setup(){           <-- private section
     const health = computed (()AppState.health)
     return{            <-- public section, need to put 'health' in both
        health,
        attack(){
            AppState.health --     <-- now object with .value property, is proxy object
            console.log('HEALTH:', health.value)    <-- .value is always unwrapped by default
        }
            }
         }
    }
* all things written to console stay in console, so need manual clear or refresh to eliminate render error
COMPUTED = "GET", not meant to be manipulated

#   - service

class _____ {


    attack(){
        AppState.health --
    }
}

back in .vue

import {computed} from 'vue'
import {AppState} from '.../AppState.js'
import {bossService} from '.../services.BossService.js'

export default {
     setup(){           <-- private section
     const health = computed (()AppState.health)
     return{            <-- public section, need to put 'health' in both
        health,
        attack(){
            bossService
            console.log('HEALTH:', health.value)    <-- .value is always unwrapped by default
        }
            }
         }
    }

Vue dev tool - target icon is to target component


back in service

class _____ {


    attack(){
        AppState.health --  <-- can also do -= for other amounts
        if(AppState.health <0){
            AppState.health = 0
        }
    }

restart(){
    AppState.health = 100
}
}

in homepage, add button to do restart AND need to add to "controller section"

import {computed} from 'vue'
import {AppState} from '.../AppState.js'
import {bossService} from '.../services.BossService.js'

export default {
     setup(){           <-- private section
     const health = computed (()AppState.health)
     return{            <-- public section, need to put 'health' in both
        health,
        attack(){
            bossService.attack()
            console.log('HEALTH:', health.value)    <-- .value is always unwrapped by default
        },
        restart(){
            bossService.restart()    <-- v-if"health == 0" to get it to show only when boss health = 0
        
        }
            }
         }
    }
disable button
    :disabled="health == 0"
        binds disabled statement to "health == 0"

*STUB - can bind classes to certain conditions so have BOTH 'class' and ':class'
class = "bg-secondary"
:class="{
    'text-success': health >=75,
    'text-warning': health >30 && health <75,
    'text-danger': health <=30    <-- conditional binding because otherwise on restart last line read is default new
    'display-1 bg-dark': health == 0
}"

bootstrap classes have specificity, so some colors will not show as class conditionals above the chosen (ie, bg-primary is more specfic than bg-secondary)
so custom CSS with '!important'

can conditionally bind styles, too  <-- all bindings must be in objects AND retain their appropriate syntax

:style="{
    backgroundColor: hralth == 0 ? 'goldenrod !important' : ''
}"
    ^ this is messy, so try to avoid when reaonable
    if put inside script, will req. health.value in computed format
console errors will keep page from being accurate, so manual refresh can bypass for code you know is correct

CTRL + SPACE to import when taking to correct component pages

/style scoped/  //script/ <--scope is to page-specific code
if you want to NOT use "scoped" do it on the main.js page

**SECTION vender example
in homepage
<div> /--   foodItem(item) loop     --/ ie v-for === foodItems.forEach
    <<foodItem v-for="item in foodItem" :key='item.id'>>   <-- these "" mean, essentially, for each
</div>                         ⬆️ this is a local variable, can be "x", or anything
</div>     ⬆️ this whole line is a template
v-for repeats whatever it is you want repeated, so careful where the line needs to be, with only the food item being in line with its details, while the times it is rendered in a style is per instance, not just one instance

each item will need an "id" id: 1
to get to APPSTATE must use COMPUTED method with anonymous f(x)n

function is set up to receive argument, can set argument later as anything
*NOTE - in Vue, arguments are called PROPS
Props are singular of object, you only get one at a time

Vue dev tools
RouterView
    homepage
        all the components listed here, so can see props

# Mick's Sept. 12 Vue lecture
use Vue-starter in BCW-create

if Code runs it vs if user runs it
if CODE runs it, then define it as a function outside the return
if USER is meant to run it, then it needs to be called within the return
    ares within the retun are are accessible by the template

#   SECTION - vueFlix - https://developer.themoviedb.org/reference/intro/getting-started
started with model - all the this.x = data.x
go to service - no changr from MVC methods
go to homepage to find a place to load
    WITHIN the return function create the function that will be @click in the HTML
        if function needs to pass parameters, you need parentheses, but w/o, you don't need them in HTML
    NOW use Vue lifecycle hooks: onMounted, onUpdated, onUnmounted
        ie: added to DOM, updated in DOM, and REMOVED from DOM
    Make async function
        relies on SERVICE business logic
    Add the relevant AXIOS
        the API has special certification paramenters (to limit the ratings parameters)
APPSTATE
    movies : []     <-- object syntax, NOT variable syntax
*REVIEW - res.data.map is NOT a function
SO - res.data.result.map <--objects do not have a map function

COMPUTED - points to a reactive piece that sets an active view to listeners
^ this connects to the APPSTATE

can stick the object(array) into the template to see if any data renders (long string of text)
in reality, will want to do a V-FOR
v-for="movie in movies" :key="movie.id" <-- keys allow unique IDs to keep data separate
{{movie.x}}
in image SRC (source)
*NOTE - BINDING data    *in between* tags uses double brackets {{}}
BINDING data *in* tags uses :

# - details
components only speak to the data within themselves
can still import data from other pages

use props to render components
pass prop data by creating an attribute that has the same name

? = Elvis operator
^ keeps code from reaching into undefined objects notation

this.genres = data.genres?map(g => g.name)

Modals are always rendered, just hidden <--that's wild


# #ANCHOR - each section has its component: Search bar

all these components will be rendered to homepage
forms are submitted on button or on enter
@submit <-- all previous "on" functions like "onSubmit" are now @, like @submit
.prevent == event.preventDefault()

can create reactive items with 'ref' w/in a setup function
^ cannot redefine the ref, bt the value of the ref
    searchTerm = "" <-- changing value

ensure env.js is aligned

v-if and v-else only work as siblings, not nested
# Mick's Wednesday lecture - Gregslist-Vue
bcw create
    vue-starter
env variables from sandbox
    incuding sandbox as baseUrl

# - router from homepage
useRouter() <-- auto nav the user
or button w/router link <-- uses PUSH method (router.push(name:'cars'))
    but button cannot tell you are going to new page
        link used whenever clicking should take you to a new place
# - carsPage.vue

setup(){
    onMounted(()=> {
        getCars(
            *any other functions you need
        )
    })

    async function getCars  <-- add to service for the logic
}

*STUB - SERVICE, APPSTATE
add API connection and place values in AppState so as to load
await api.get('api/cars')
AppState.cars = res.data.map(car => new Car(car))
    always check res.data before saving to appstate
        looking for array in map
use Vue tools to see them in APPSTATE

must compute to get it out of APPSTATE and onto PAGE via TEMPLATE
    Must place the compute in the RETURN
        what is in setup is visible to code
            in return, accessible by template
setup(){
    onMounted(()=> {
        getCars(
            *any other functions you need
        )
    })

    async function getCars  <-- add to service for the logic
    async function getCars() {
        try {
            await carsService.getcars()
        } catch(error){
            Pop.error(error)
        }
    }


    return{
        cars: computed(()=>AppStae.cars)
    }
}


# - template
⬇️ this is placed WITHIN div tag
v-for="car in cars" :key"car.id"    <-- keeps track of item by ID
{{data dump between tags to test}}  <-- this will let you know if you can even render any of the retrieved data

CarsPage is all while CarCard is a single car (item).

Make sure the carCard has PROPS
    to pass data from the page into each individual component
        carCard will be same for each car, with interchangeable data
    
*NOTE - The carsPage has data, so throw the carCard in there
<carCard :car="car" />  <--data bind, gets data for each iteration of for loop

    export default {
props: {car: {type: Car, required: true}}
setup(){
    return{}
}
    }
on carCard page, determine the look of the template - what will be drawn to the carsPage

# - SCSS
&:hover

g-3 = gap distance 3 <-- adds margin and padding to column - only works if content is inside a box (card elements)

# - car details page (carDetailsPage.vue)

add path in router
path: '/cars/:carId'
name: 'Car Details'
component: loadPage('CarDetailsPage')

throw router link in the CarCard
<router-link> works, throw :to {} into tag
    these have params, so make sure the params are filled out, or else will throw error

*NOTE - carsPage gets the car, not the car details card
only contains info required to show/use

PAGES NEVER TAKE IN PROPS
    can, technically, but,...don't

# - ID in url benefits
Need ability to independently load a page without navigating from home site
*STUB - there is ROUTE and ROUTER
    route is where you are
    router takes you elsewhere
incarDetailsPage

const route = useRoute()
onMounted(()=> {
    getCarById()
    logger.log(route)
   async function getCarById(){
    try {
const carId = route.params.carId
await carsService.....
...
    } catch (error)
{

}   }
})

throw :src to trigger activeCar.imgUrl
# - #SECTION forms in Vue

vue in COMPONENTS
 throw data in template
const carData = ref('') <-- in setup, AND return
async createCar()   <-- this in in the RETURN since it is user-based
    use router.push(takes item, and params)
        ⬆️ taking you somewhere, so routeR, not route
@submit.prevent

in SERVICE
add
    RETURN res.data.id
        or even const newCar = res.data
            RETURN newCar
create and push are a;most separate, so code and test in parts
    the car must actually be being made before you can ID or call it


CLONE THIS DOWN

# Mick's Thursday Sept. 13 lecture - Project
SANDBOX - final object is an array

endpoint uses query api/profiles?query=mick

be sure when you log in you have the token, userinfo, and account loading

# - design
Homepage redesign
Create MODEL for project
Create SERVICE
    api.get
        logger <--check to see if res.data is being retrieved
    This function will be called in HomePage

HomePage - onMounted
                getProjects
    SERVICE to APPSTATE
Homepage w/in RETURN block COMPUTED
    draws info from APPSTATE
{{projects}}    <-- dir into Homepage template to test that info is coming through

#SECTION - layout

Section--row
    Div--col, v-for="project in projects" :key="project.id" <--d-flex can go in WITH col
            {{deets A}} {{deets B}} <--call these in COMPONENT (should see double entry on page) before commenting out

#SECTION - MAKE COMPONENTS (card time)
Project card
#NOTE - TURN OFF JS setting in imports

Props go here <-- want to retrieve full item
    will need to be passed as argement in SETUP to be called in RETURN
        //NOTE - computed elements must be pre-rendered to your desire w/ styling all already in place
v-bind takes values in the RETURN and passes them as styling
# - Modal wrappers: slot tags
Slot in a template into another template
Style like router-link w/ open and close tags

in Modal, use slot tags, into which you place div or button or whatever
    can tag into the MODAL wrapper using template #<--to id which portion of the wrapper you wish to draw in/fill out


remember the v-if="activeX", so that things will load only when active is chosen, vs auto-breaking upon page load

be sure to temember you van use queries in the endpoints w/ string interpolation
ProjectCard :project="project"
                        ⬆️ this is what they ahve the option to pull from

# service
    .map --> creates new array
        cannot map a single object, must be an array of objects

        if there is an undefined or null, use elvis operator so that code will not try to reach into an undefined or null object for a value that does not exist and then break code
# #STUB - Changing account info

