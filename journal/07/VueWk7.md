Account page <-- place form here

put max-length on both front and back end

*****************
WEEK 7 - Friday checkpoint introduction
*****************

# Mick's Monday fullstack vue lecture

BCW-create
express-vue

worskspace file
npm i this

ENV with the gear icon -->mongoDB
ENV.js sandbox info (from Auth0)

MAKE SURE YOU HAVE 200 on all the user, token, account requests

# - in Postman
DO NOT CHANGE THE TESTS
    copy to new folder if you want, but leave the test bank alone
        these will affect your server, backend connectivity
            NEED to be able to CREATE somethong
                otherwise no test will be able to be run - no data
        Tests are largely heirarchical, go in order
            many will not work if previous tests were not passed

albums - pictures are one to many
collaboarators are many to many
    you can collaborate on many albums
    albums can have many collaborators

server and client go to server, client side

# - Model
exporst const AlbumSchema = new Schema({
    <!-- do not need constructor in backend Schema -->
    title: {type: String, required: true, maxLength: 100}
    category:{type: string, enum:['x', 'y', 'z'], lowercase: true}
    <!-- can pass all entered data to lowercase for the model ⬆️ -->
    coverImg: {type: String, required: true, maxLength: 500}
    creatorId:{type: Schema.Types.ObjectId, ref: 'Account', required: true, maxLength: 100}
    archived: {type: Boolean, require: true, default:false}
},
<!-- can now pass objects -->
{timestamps: true, toJSON: {virtuals:true}}
)
AlbumsSchema.virtual('creator'{
    localField: 'creatorId',
    foreignField: '_id',
    ref: 'Account',
    justOne: true
})


ADD TO DBContext
ref is plural, (left side)

# CONTROLLER and SERVICE
C
export class AlbumsController extends BaseController{
    constructor(){
        super('api/albums')
        this.router

        .use(Auth0Provider.getAuthorizedUserInfo)
        .post('', this.createAlbum)
    }
}

async createAlbum(req, res, next)
try{
    let albumBody = req.body
    albumBody.creatorId = req.userInfo.id
    <!-- all this ⬆️ is necessary to verify before moving forward -->
    const album - await albusmsService.createAlbum(albumBody)
    res.send(albumBody)
}catch(error){
    next(error)
}

S
class AlbumService{
    async createAlbum{
const album = await dbcontext.Albums.create(albumBody)
<!-- in CREATE must await populate (nothing is there before into which to populate) -->
await album.populate('creator')
}
}

in these tests you will find the data you need to call to solve the problems necessary (esp later on)

# in Postman
variables - fill in authorization tokens here
    take token from DEV TOOLS NETWORK tab
        place in both current and initial value

the .get function - use query

anytime you use a find you tack the .populate('') to the end
create or update you need to put it on its own line

.get('/:albumId', this.getAlbumById)
 C   will pass in (req.params)
 S   (albumId){
    const album = await sbContec.Albums.findById(albumId)/populate('creator')
if(!album){
    <!-- NULL CHECK -->
    throw BadRequest('no album at id: S{albumId}')
}
<!-- must return -->
    return album
 }

 # - Delete req for archival method
    sites do not delete your content from their site - they archive it
        soft delete
            hide from front end
        removed from live database and put into archived database
    
the server side is adjusting, but the functionality is the same as a delete
    just like the post req for 'liking' in last checkpoint was a "post" to the user, no data was manipulated - body remains same

    send two things down

    const album = await albumsService.archiveAlbum(req.params.albumId, req.userInfo.id)
Only certain people can be authorized to delete stuff ⬆️

    in service
    *NOTE - can await prior written functions
     archiveAlbum(albumId, userId){
        const album = await this.getAlbumById(albumId)
        if(album.creatorId !-userId){
            throw new Forbidden('nacho purse to mess with!')
        }
        <!-- album.remove( for actual deletion) -->  // we, and few, ever use this
        album.archived = !album.archived
        await album.save()  <-- after above is done, can re-load
        return album    <-- double checks the method, return proves get works
     }

# pivot to pictures
notice the arguments being passed in the functions in the CONTROLLER and the methods deployed in the SERVICE

can run functions from other services as verifiers - we do not need it to fully run in present service
getPictuesInAlbum(albumId){
    await albumsService.getAlbumsById(albumId)
    <!-- an album IS  returned, but the main thing is running here to verify info, and we can do this, yay -->
}

the issue arises if a new DBContext or repository is being referenced, but the SERVICES can talk all they like
CONTROLLERS should NOT talk to other CONTROLLERS, though they can talk to any SERVICE they please, too

# - Bad Requests for Bad Actors
Inadvertant and malicious users

two diffwrent tokens to test evil_auth
    *NOTE - use an incognito tab

About 70% of app can be designed on the front end with just th bare bones of the SERVER side requests made
    I can do the POST and two GET req to do this
        front end will take far more time to handle
# ******************FRONT END

in client folder - all server folders closed and tab bar closed.

Homepage - tack on the methods for getAlbums()
    need a MODEL, SERVICE, AppState
Vue --> App

v-for <-- forEach
    try to render just one thing first
    v-for="a in albums" :key="a = a.Id"
    {{put a single piece of data in here}}

this is the hompeage

*NOTE - cannot render card to Home Page w/o the PROPS being put into the AbumCard
    this is not the abiltiy to draw
        can create an album card without req props - could break not placed.
After this, you could 'cause problems' with required props not being present to render sort of breakign the code
be sure to make sure the data and naming conventions are correct
    "a" is a whole album, here, so be sure when the component draws that the information being passed down, but the name can change
        think of renaming an old moving box
    props passed can then allow readable input

here will be more parallel to last checkpoint in finding styling and errors


const filter by = ref({})
@click="filter by = 'animals'"
^ this allows for the particular button to draw to page the specific categories to same page
kind of like the search bar, but with preset

    #SECTION - the details

*NOTE - computed requests can take multiple arguments
albums: computed(()=> {
    if(!filterBy.value){
        retunr AppState.albums
    } else {
        return AppState.albums.filter(album => album.category ==filterBy.value)
    }
})

The filterBy method is a REF, a watchable object, which is reactive


# *******continue PostIt lecture from Monday
WILL use MODAL
    bs-5-modal  <--SNIPPET
take out footer
    put in SLOT sections (slot name="header", name="body")

        ⬇️this allows you to make info interchangeable across all modals
props: {id{type: String, required: true}, showButton:{type: Boolean}}}   
    data bind --> :data-bs-target="`#${id}`"

: <-- passes computed data

beginning and end tag if you want to define what will go in slots
NO: <modalWrapper />
YES: <<modalWrapper></modalWrapper>
YES: <<modalWrapper id="create-modal">
template # header
    i class
template

template # body
    i class
template


</modalWrapper>

# #SECTION - albumForm.vue

create album? Need form

⬇️ this works well for enum properties where you do not want people guessing the appropriate 
SELECT tag
    OPTION value="a"
    OPTION value="b"
⬆️ good for setting dropdown options
    form creating album within those categories
        value="" <-- empty string placeholder can be Please select a category
    To do that A

            function resetForm(){
                albumData.value = {category: ''}
            }
            onMounted(()=> {
                resetForm()
            })


*NOTE - album form component

create function be sure to pass on argument with .value ie. albumData.value

resetForm() should work within the RETURN block functions

on the @submit.prevent="createAlbum"    <-- no parentheses needed to call form


UNSHIFT puts newest at the top
PUSH puts newest at bottom

can SORT('').populate('')
⬆️ sorted "-createdAt" takes newest first

useRoute() route params are set in the router.js

#STUB - in APPSTATE
{} <--truthy
null <--falsey

# NOTE - picture model
some classes are already in existence, be mindful of this in madel naming conventions
# SECTION - album service
map is for array
res.data can open directly into array
    no nesting under new data piece, ie results, posts, likeIds

css: width: 100%
aspect-ratio:1/1

p tags have margin

# NOTE masonry format
CSS
    can nest
    columns: 200px
    img{
        width:100%
    }

pre-rendering will return null
    v-if="album"    <-- basically an await for when the page loads and verifies the draws/gets

*NOTE -     preview picture using data bind :src=pictureData.ingUrl

# ***********BACK TO SERVER SIDE
make collaborator MODEL

we are only accessing the connection between the two - albums and account

will need virtuals

now make controller and service

⬇️find the match
{{accountId: userId}}
OR just pass accountId into argument of getCollaborationsByAccount and .find(accountId)

in many-to-many find out what info the Postman test actually wants back?

# 2nd virtual in Album
AlbumSchema.virtual('memberCount', {
    localField: '_id',  <!-- these first two are flip-flopped from the other virtual, looking the opposite way, reverse ID from Collaborator virtual-->
    foreignFiled:'albumId',
    ref: 'Collaborator',
    count:true  <!--creates a nubmer for each matching document (each collab w/ albumId rhat matches the album's ID)-->

})
*NOTE - WHAT ARE YOU LOOKING FOR?
Album is looking through the COllaborator collection for its owm album ID in them
    parent object looking at child object
MUST populate virtuals
    can simply add to .populate arguments

.populate({path: 'album', populate: {path: 'creatpr memberCount', select: '-email'}})


Check network request orders if you get 'unauthorized' errors
*NOTE - cannot get account info on page load - will return unauthorized

# auth service
IN SuthService.on(){


    last line write new lines
}


BE CAREFUL WITH CASCADING CONSTRUCTOR INFO
props: {album: {type: Album || Object, required: true}}


# * STUB
abstract into a computed:
isCollaborator : computed(()=> AppState.activeAlbumCollaborator.find(collab => collab.accountOd == AppState.account.id))
    NOW can run as a param for the truthy-falsey in a v-bind
add a v-else, too,that will remove
    needs own function to reverse call
        deleting a RELATIONSHIP not an object

can v-bind multiple
    v-if="!isCollaborator && user.isAuthenticated"

# ******NOTE  Maybe a watchEffect can bypass the server reload that allows duplcation of collaborators?
onMounteddoes not run with change of route.params, so 
# router push after creation
router.oush({name: 'Album Details', params: {albumId: newAlbum.id}})
    got newAlbum from a return in the SERVICE


ATTEND button will have a lot of conditions: are you going, is the event full, attending, ..... can wrap, v-if et al,

19 req for this

# Postman tests
*NOTE - events cannot be deleted, only cancelled
Hot link

JSON text is not what you want
    JUST take LINK URL
        My Workplace
            Import
                paste URL
                    Should have Tower tests show up
                        Open TOWER folder
                            Authorizations
                                Reg auth token & Evil auth token
                Run tests in order
                    figure out what you need to be passing in order to pas req beyond Postman
                        You want tests passing, but fill out the other stuff
                            Event endpoints good?
                                go and develop the front end for that portion of app

                                *NOTE - Cancel and delete is hard - no examples, leave til later and ask for help