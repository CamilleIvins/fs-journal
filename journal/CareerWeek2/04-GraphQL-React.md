#   Mark Ohnsman - Creating Scalable Apps Ready for Microservices
************************
Typescript NestJS GraphQL
Chief - NYC Executive women's social network
    - used to work for 
studio.apollographql.com
docs.nestjs.com

**ADVICE**
Build GregsList in whichever framework or language and utilise at least one relationship
#
# - Typescript
"Microsoft's attempt to turn C# into JS"

Odds are JS will be the only language you still learn, but know the similarities via patterns

JS 2.0 essentially
Most used, even over JS

JS is more learnable and has broad browser compatibility
TS - team collab and larger projects
# NestJS
Node.js framework on top of express

Express JS is for simplicity
NestJS is more structured and scalable
# GraphQL
Query language for your API
Specify exact data - and nothing more
Apollo API - can link to Github
# studio.apollographql.com, docs.nestjs.com

When to use GraphQL vs standard REST
    - complex APIs with a lot of relationships
        - graphQL will only get the data that you need
REST - straightforward? = use REST

# Learn how to write tests
Key to comprehending code // what Fortress InfoSec said
# GraphQL GregsList
SRC
    Main.ts & app.module.ts
    Create Modules folder
        Cars
            car.module.ts (files imported via module)
            car.service.ts
            car.resolver.ts <-- //MVC Controller
                (client hits this first)
            car.type.ts

car.module.ts
    @module{
            imports: []
            providers: []
            }
            export class CarModule {}

car.service.ts
car.resolver.ts
where you drop in "const =" to hard code an instance

car.type.ts
// schema (query type, NOT database type)
@ObjectType("____") <-- can leave empty
export class Car {
    @Field{(=> Int, {nullable: true})} <-- lets return if no data
    will default a few import types
}

app.module.ts
@module {
    imports: [CarModule]    <-- must be included to get app-wide import
}

@mutations = post, put, delete
! to make required w/in create format

w/in Comments type, can specify relationship type "@ManyToOne"
