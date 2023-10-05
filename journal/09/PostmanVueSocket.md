# Postman GregsList Test Lecture

in Variables - Endpoint
    Initial value - http://localhost:3000
        Live version? - ie= https://livesite.com
    Auth - get yours sorted with Mick/someone

Now, in your test request
{{endpoint}}/api/cars

raw, JSON data
"make": "aston martin"
"year": 2021
....
Auth - token: {{auth}}

Tests - js - type a console log - runs after request
UNLESS
console.log("run before request")

#   pm
"pm" is a Postman script
    Mocha and Chai testing frameworks
        Chai is an assertion library
            running off of Mocha

    const res = pm.response.json()
    console.log("res", res)

To

    const res = pm.response
    const body = res.json()
    console.log("reponse", res, body)

(mini test)
    if(res.code != 200){
        console.error("Bruh, nah")
    }


const req = pm.request
const original - JSON.parse(req.body.raw)
console.log('request', req, original)
#   Making a test
 
 <!--           ⬇️ this is the test name -->
pm.test('Request was a good one', ()=> {
    const goodOne = res.code == 200 <!-- truthy-falsey-->
                                <!--⬇️ this os a term, we stopped using-->
    <!-- pm.expect(goodOne).to.be.true(['Was not a good one') -->
    pm.expect(goodOne).to.be.oneOf([200, 201],'This means the request failed, check console log for details')
    if(res.code != 200){
        console.error("Bruh, nah")
    }
})

pm.test('Car created as ecpected', ()=> {
    pm.expect(body.make).to.be.eql('aston martin', 'Make of the car was wrong')
    pm.expect(body.year).to.be.eql(2021 || or || original.year, 'Year of the car was wrong')
    ...all the rest
})

#   Get request

Get by ID

{{endpoint}}/api/cars/________<--ID

const res = pm.response
const car = res.json()

pm.test("Got ze right car" () => {
    pm.expect(car.id).to.be.eql('{{ID}}', "This is not the right car")
})


#   pre-request script

THIS IS WHAT *AXIOS* SAVES YOU FROM HAVING TO DO

let config - {
    'Content-Type': 'application/json'
    url: `${pm.variable.get('endpoint')}/api/cars
    method: 'POST',
    hrader: {
        Authorization: 'Bearer' + pm.variables.get('auth')
    },
    body: {
        mode:'raw'
        raw: JSON.stringify(carData)
    }
}

pm.sendRequest(config)

# Vue Tour
use read me to install
v-tour
    steps
        steps point to target (what actions will display)
        
make sure you are cd-d into the client side of the folder
    npm install vue3-tour
        visible in package json file

main.js

cosnt root = createApp(App)
registerGlobalComponents(root)

root {
    .use(router)
    .use(Vue3Tour)
    .mount(`#app)
    }

#   in homepage

steps:[{
    target: '#v-step-0' <-- where this is activated, mutli-step == || a tutorial
    header:{title: ''}
    content: ''
    actions:{next: ''}
    params:{placement: ''}
}]

tourCallbacks:{
    onFinish: (()=>{
        router.push({name: 'Album Details', params:{{albumId: AppState.albums[0].id}}})
    })
}

in v-tour div :callbacks=''

#   Tour.vue page

<v-tour name='myTours' :steps="ssteps" :callbacks="tourCallbacks">

props:{
    steps: {type: Array, required: true}
    callbacks: {type: Object}
}

mounted{
    this.$tours['myTour'].start
}

# limit tutorial via account page

.put(this.updateAccount)

in server side

async(req,res,next){
    try {
        const account = await accountService
    }
}

in client side
async editAccount(){
    trycatch
}


onSkip(()=.{
    await accountService.editAccount({neetsTour:false})
})