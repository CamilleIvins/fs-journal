# Sam's Tuesday Sept 12th fireside
redoing Pokedex with pagination techniques that will be useful for checkpoint

   # #SECTION - bcw create vue-starter

NEW api axios instance for the pokeapi.co
first link given is paginated(shows full number of pages <-- view is 20/pg)

spin client, localhost:8080

   # #SECTION - Homepage: setup

export default{
    setup(){
        ALL FUNCTIONS GO HERE
            will be async, so try-catch, await

    onMounted(()=> {    <-- this is the draw function
        function,
    })

     return{}
    }
}
   # #SECTION - service

   need to inport this manually into Homepage to use in script section
   service methods do not change from MVC
   
   logger the request and see if the information goes to console (ie, is being successfully retrieved)


place data on homepage template where you will want it
class by style using the SCSS at the bottom of page


   # #SECTION - AppState

save data to APPSTATE by throwing SERVICE data retrieved from API into it via AppStae.x = res.data

Vue dev tools - look in App and flip through lower nesting

BACK TO SERVICE

export default{
    setup(){
        ALL FUNCTIONS GO HERE
            will be async, so try-catch, await

    onMounted(()=> {    <-- this is the draw function
        function,
    })

     return{
        ⬇️ banana word
        pokemon : computed(()=>AppState.pokemons)
     }
    }
}

computed is like a built in listener for appstate

raw data dump by {{x}} into page

#STUB - scss
    overflow-y: scroll

   # #SECTION - v-for
   v-for="pokemon in pokemons" :key="pokemon.name"
   {{pokemon.name}} BETWEEN the tags, NOT inside

   # #SECTION - @click
   @click='setActive(pokemon.url)'
                ⬆️ place in return, because will be called, need async method
                export default{
    setup(){
        ALL FUNCTIONS GO HERE
            will be async, so try-catch, await

    onMounted(()=> {    <-- this is the draw function
        function,
    })

     return{
        ⬇️ banana word
        pokemon : computed(()=>AppState.pokemons)

        async setActive(pokemonUrl)     <-- w/in return block, so not 'async function', just 'async'
     }
    }
}
   # #SECTION - AppState
build model based on returned data


Be sure APPSTATE also has
    activePokemon = null
NOW need to v-if="active", or else will nto render due to activePokemon being null in AppState


   # #SECTION - active vue page

all script logic must match the vue page, or else will not connect
*LINK - none of the imports auto import, so many things will be "x is not defined"

   # #SECTION - pages

in APPSTATE
nextUrl = res.data.nextUrl
previousUrl = res.data.previousUrl

so now can add function in RETURN where user can interact with it
    try-catch
    throw in logger
    @click="pageChange()"
        compute in return the next and prev
            can now pass argument
                :disabled="!previous"
    await w/ passing of entire URL into service
        const res = await axios.get(url)    <--w/ one api in axios


Compare the getPokemon and changePage SERVICE functions