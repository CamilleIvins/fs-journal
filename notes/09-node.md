# Node 
Place in ENV file connection string
**Connection String: mongodb+srv://student:lH4VTMYtunNzWu8o@bcwdatabase.25sxqum.mongodb.net/?retryWrites=true&w=majority **
                                    ⬆️user|   ⬆️password  |

Postman API key:
PMAK-64f7f58f7a63e400439bd5f1-c0fb9f478448cfbeb568b6798dc6b41dee

Not sure if this is important:
{
    "collection": {
        "id": "00800b4a-d0b6-40fb-8ff4-ea01ad49951a",
        "name": "{{collectionName}}",
        "uid": "29547431-00800b4a-d0b6-40fb-8ff4-ea01ad49951a"
    }
}
Tutor@Help.com //TutoringSesh@Help.com //MoreTutor@Help.com <--Tutoring?
HelpMe
TutorM3!
# Mick's Tuesday Sept. 5th lecture
castle analogy
routes and channels
Middleware - ie formatter, authorizations (auth0 --> can send a 401)
   #  SECTION - node-server-auth0
   express server - no front-end (no CSS work)

   // MVC design pattern but w/o APPSTATE

   bulk of code will be in server folder
   SERVICE
   CONTROLLER - acts same way, but does diff stuff
    still links to API end points
    this.router is NOT *a* router, but the route to the endpoint
    code runs at this point to determine ability to do anything at the endpoint (ie get, put...)
   MODEL - document database --> mongoDB 
    Schemas, new Schema, not Model

debug console will // the browser (on "run"? tab) run and start server

serving on port 3000
    ^ running in background
        ^localhost:3000
            ^server has other routes, so can /api/____ <--- use like a door, a-tag, portal, etc
   #  SECTION - example w/ cats CONTROLLER
CatsController
*NOTE -                        ⬇️ inheritance, ie species inherits traits from genus
export class CatsController extends BaseController{
constructor() {

}
}
contructor will look weird - red squigglies all around

BaseController registers the CONTROLLER with the express
    ^ directions for the hallways, keypads for the keycards
        ^done for automation, so every CONTROLLER after INHERITS the map of the BASECONTROLLER

export class CatsController extends BaseController{
constructor() {
    super() <--super calls the constructor of the BASECONTROLLER
}
}

export class CatsController extends BaseController{
constructor() {
    super('api/cats') <--super is the signage of the route code will go through
    this.router     <--subroute of the API route
    .get('',()=>console.log(`they be gettin' cats`))  <-- 'are you actually going to extend this path', function (currently anonymous for lecture)

}
}
*NOTE - can only see changes when refreshing - from debugger tab, will get little window, too for the stop and refresh
*NOTE -  server is separate from broswer, so console log will show up in DEBUG console

export class CatsController extends BaseController{
constructor() {
    super('api/cats') <--super is the signage of the route code will go through
    this.router     <--subroute of the API route
    .get('',this.getCats)  <-- no extention, function called

}
}
getCats() { <--3 parameters allowed
    console.log(`they be gettin' cats`)
}

request = object representing the incoming request from user
response = object (of response) for you to manipulate and use to send response to requestor
next - how we kick people back out of the endpoint (hallway)
⬇️
getCats(request, response, next) { 
   response.send(`you got cats`)
}
    ^ this will show in broswer

    *NOTE - can stylize here
getCats(request, response, next) { 
   response.send(`<h3>you got cats</h3>`)
}
    ^ this will show in broswer

npm run start from command line can run through the data from project, prove it is there, even when console will not show
^TEDIOUS

getCats(request, response, next) { 
    console.log(`they be gettin' cats`)

logger.log(request )        <-- can see info on the request going in

   response.send(`<h3>you got cats</h3>`)
}

   #  SECTION - example w/ cats SERVICE

const fakeDB = {
    cats:[
        {name:'Schnapps', age:2, color:'Calico'},
        {name:'Marcuse', age:1, color:'Orange'},
        {name:'Todd', age:7, color:'Black'},
        {name:'Lupine', age:3.5, color:'White'},
    ]
}

class CatsService{
const cats = fakeDB.cats
return cats <--must be returned to controller so CONTROLLER can send through
}

export const catsService = new CatsService

in CONTROLLER

getCats(request, response, next) { 
    console.log(`they be gettin' cats`)

logger.log(request )        <-- can see info on the request going in
const cats = catsService.getCats()
   response.send(`<h3>you got cats</h3>`)
}

getCatByName(request, response, next) {
    const cat = catsService.getCatByName()  <-- need to know what you are talking about in order to get this to work
    response.send(`getting cat by name`)
}


SO 
change routes in CONTROLLER constructor
export class CatsController extends BaseController{
constructor() {
    super('api/cats') <--super calls the constructor of the BASECONTROLLER
    .get('', this.getCats)
    .get('/:catName', this.getCatByName)
    }
}

getCatByName(request, response, next) {
   logger.log(reqest.params)
    response.send(`getting cat by name` + request.params.catName)   <--browsers as string
}

getCatByName(request, response, next) {
   const cat = catsService.getCatByName(request.params.catName)
   logger.log(reqest.params)
    response.send(`getting cat by name` + request.params.catName)   <--browsers as string
}

in service
const cat = fakeCB.cats.find(c=> cat.name == catName)
return cat

getCatByName(request, response, next) {
   const cat = catsService.getCatByName(request.params.catName)
   logger.log(reqest.params)
    response.send(cat)   <--browsers recognizes and allows 200 'okay'
}

*NOTE - with misspellings you can still get 200s, so we need to let user know request was bad
if(!cat){
    return no cat   <-- so need error handler
}
if(!cat){
    throw error('no cat')   <-- keep TRYCATCH
}

getCatByName(request, response, next) {
    try{
   logger.log(reqest.params)
   const cat = catsService.getCatByName(request.params.catName)
    response.send(cat)   <--browsers recognizes and allows 200 'okay'

    } catch (error){
        next(error)   <--lets user know which error, not a 200 response
    }
}
   #  SECTION - utils

different error classes listed out to use ie BadRequest
404 is wild router route
so 400 it as and give a reason('' + ___)

can go into errors and script your own error codes, usually in the 400s
   #  SECTION - mongoDB.com/cloud/atlas

google mongodb atlas --> start free
sign in with git or gmail, git will be fine
*NOTE - *you can make your server anywhere in the world*

# - Gregslist w/Node
CONTROLLER w/ BASECONTROLLER
//todos - create a model first (POST request)


constructor
    super('api/cars')
    this.router
    .post()

using URLS is a GET request, so you 

   #  SECTION - postman.com
   postman acts as middleman to get these
   downloaded, same credentials - will one day need to transfer account info to NOT personal e-mail, perhaps 
   #  SECTION - Order C->M->S, MODEL

create the model w/ data values         ⬇️differentiates from simply saying "number" or "string"
can define values further ie: price --> {type:number, required:true}
⬇️one word
Max length on strings is impirtant, so JSON.stringify is not used to take up whole memory
color set to max and min length = 7 restricts to hexcodes


now need to register schemas to database in DbContext file

all new data will flow through from service
    operators in this section are legion, here ⬇️ built in from Mongoose (ORM object relational mapper) allows framework to talk to to doc database
            const car -= await dbContext.Cars.create(carData)

also new w/SERVICES

use FIND to get a list of documents, cs in JS where you get ONE thing
    ^ also cannot pass through functions

    it is not easy to merge collections, so be sure that the DbContext collection is unified
on DELETE w/o ID, it is implied you delete the full array, so remember to enter

most clear solution is the specific way -->findById (gets single item)

# Sam's Tuesday fireside
Building NODE side of Inspire - checkpoint 4

using EXPRESS-MVC
    NODE and using auth client-side
            local host 8080 is embedded in this client side, has app
            this client allows for log-in
server side has the env for the mongoDB
use same domain, auth, and audience keys as before

start server from debug on lefthand tab

    #SECTION - making schema
This is the model - with constructor and enbedded super
const Schema = mongoose.Schema

dbContext - does not know about MODEL....so add

NOW

pull up MongoDB
            ^ saves as docs, not JS

can make CONTROLLER & SERVICE

router in constructor registers requests - your doorman

#STUB - start w/ post request

talking w/ auth0
.use    <--bouncer
.use(Auth0Provider.getAuthorizedUserInfo)   <--which you get from info baed on login as seen when logged or in network
.post()
.get
.push



right under router start .post (create function)
// the create for GregsListNODE for sure

in SERVICE
dbContext // AppState

TONIGHT
in postman http://localhost:3000/api/cars

can take bearer token from network and put into authorization tab in postman


The little red dots that make breakpoints are for when running the debugger serve

# Sam's Wednesday Spet. 6th lecture - (data) Relationships
using _LUCID CHARTS_ UML diagrammer site

one-to-one is a school to itself
one-to-many is the courses that a school hosts
many-to-many is students to courses
enum[]  <---options

arrows go in the direction of dependency (courses need a school)
#   #SECTION - start in ENV, put in connection string
nothing will work without it
create a new collection in MongoDB database by rewriting the area in key before '?retryWrites'

go to STARTUP.JS and comment out auth middleware

make SCHEMA in the MODELS page
    import mongoose
    const Schema = mongoose.Schema

    export const ExhibitSchema = new Schema ({
        this is where things like name or location go
            name: {type: string,....}
            biome: {type: string, enum: ["location a", "location b",...]}
    })

DbContext <-- register new MODEL to mongoose
#   #SECTION - CONTROLLER and SERVICE time
remember to draw in the BASECONTROLLER (and its SUPER (url endpoint) in constructor)

in CONSTRUCTOR also include
this.router
.post('', this.createExhibit)

async createExhibit(request, response, next){
    try {
        const body = request.body
        const newExhibit = await exhibitsService.createExhibit(body)
        response.send(newExhibit)   <--needs argument to work
    } catch (error) {
        next(error)
    }
}

in SERVICE
async createExhibit(request, response, next){
    const newExhibit = await dbContect.Exhibits.create(body)
    return newExhibit
}

# #SECTION - POSTMAN
Sam uses the desktop, not app

NEW
    COLLECTION
        name it
in COLLECTION
    new request
        POST    localhost3000/api/exhibits
            BODY
                RAW
                    Text -->JSON
{
    "name": "Rainforest Cabana"
    "emoji": "🌴🥥"
    "biome": "tropical"
}
    ^ send it, then can swap out values to create a new one to send

On order to see, must create a get request in CONTROLLER and SERVICE
FIND in SERVICE is a pull for full array

BACK in POSTMAN
add request

just send up GET request
    That said...
        extend by extending URL via query '?biome=tropical'
            AND
                in the async GET in CONTROLLER immediately after TRY
                    const query = request.query <--or in the controller request.query in FIND argument
                        the change in SERVICE is that the argument will not be empty, but be 'query'
                        add breakpoint <-- red dot that is same as debugger on left of code line numbers
 *TODO -        remember to respin server
                        hit SEND in POSTMAN
# #STUB - add the animals
make new SCHEMA and add to DBCONTEXT
in BOOLEAN also include default either true or false
when ref another SCHEMA -------------------------------⬇️ must match DBCONTEXT collection string
    ie: exhibitId: {type: Schema.Types.ObjectId, ref:'Exhibit', required: true}


   #SECTION -  CONTROLLER and SERVICE
*NOTE - post requests always have a BODY

#LINK - when the default of a boolean is set, you do not need to add it to the POSTMAN
extending URLs with large strings is tedious <--make RESTful endpoints
SO
set a virtual
    GO TO the Value.js
        copy the timestamp/toJSON <-- just need toJSON {toJSON: {virtuals:true}}
            put it onto the referential SCHEMA
                NEW method
                AnimalSchema.virtual('exhibit',{
                    localField: 'exhibitId',
                    ref: 'Exhibit',
                    foreginField: '_id',
                    justOne: true
                })
        go back to CONTROLLER and SERVICE get requests to perform this one-to-any request (show exhibit details as sub-object)
            in CONTROLLER constructor, give a new GET with endpoint ('/:exhibitId/animals')

*NOTE - Um, today is day one of period, and very bad cramps are cramping your note-taking ability, right now.
    PUT request // POST request
        replaces the same base info, so ALSO has a BODY
            const updates = request.body
            const echibitId = request.params.exhibitId
            const editedExhibit = await exhibitsService.editExhibit(exhibitId, updates)
            response.send(editedExhibit)
        to replace an item, you MUST get the original   -------------⬆️
        
        in SERVICE const both the 'originalExhibit' and the 'updates'
        if(!originalExhibit) throw new Error ('unable to find exhibit at ${exhibitId}')
        originalExhibit.name = updates.name <--can leave out any property you do not want users to be able to edit
        originalExhibit.emoji = update.emoji || original.emoji  <--pipe operators do not work on BOOLEAN or empty string/null
        originalExhibit.emoji = update.emoji !=undefined? update.emoji : original.emoji
        originalExhibit.emoji = update.emoji ?? update.emoji (this is coalescence, not supported on this version of template)

# - Mick's Thursday lecture
express-MVC <--fullStack application development
*creates a worskspace   <-- multiple projects in one vs code window
*this is two projects
*.client is the MVC
    in debugger, can open server or MVC
        BUT need to be in correct workspace level

fill in ENV Auth0 info
Start up BOTH server and client
dev tools --> network --> attempt login
your auth0 signin details will be in url base
if token and userinfo are 200, but account is red, problem is your login stuff
if those do, problem is Auth0

logging into auth0 stores your data one place, the extend userInfo rule is in there to sync the IDs across the local and Auth0 saves

#   #SECTION - many-to-many
Birdwatcher app
can see two things at one time, cannot be in two places at one time
account and bird know nothing about each other middleman model tracks the relationship.

BE TIDY
    - you have both ends of stack here, so only open one set of files at a time if you can
    - naming conventions matter
    -you can delete all the 'value' files <-- they are examples to show API working
        - MUST delete all references to them, though, or else errors
