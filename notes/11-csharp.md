# CSharp
Week 10 - Post-It C#
Week 11 - Instacult C#
(dotnet-vue)

dotnet goes to https://localhost:7045
to see documentation of what's going on: https://localhost:7045/swagger.index.html

Cap each word, including first

Console.WriteLine("Hello, world")

can, but don't
<!-- variable w/ no data type -->
var x = 10;
<!-- the new best practice is to declare everything STRICTLY w/ data types -->
<!-- ie, this is an integer, so "int" -->
int y = 10;
4.5 is not an integer, sp no 'int'
<!-- floats will work fine for anthing with 2 decimals -->
<!-- JS is not bad w/ math, floats are bad at math, most languages have floats -->
float z = 4.5f;
double a = 5.55;
<!-- m stands for money - transactions use decimals -->
decimal b = 6.80912m;

Strings!
<!-- MUST use double quotes -->
string greeting = "hello";
<!-- strings can be single characters, but...⬇️ -->
<!-- single characters are single quote -->
char g = 'g';

bool okay = true;
bool no = false;

Arrays are not cool - C# arrays are less common
They do not work the same way
# Problem being: C# arrays have fixed lengths that cannot be modified
<!-- Array<int>[3] = new Array<int>[3]{1, 2, 3} -->

#   Lists
Work like arrays in JS
<!-- List is the complex data type, what is in <> is the type w/in, ie, the parameters of a data type -->
<!-- Complex data types are all classes -->
List<string>cats = new List<string>();
cats.Add('Schnapps');
cats.Add('Marcuse');
cats.Add('Lupine');

Console.WriteLine(cats.Count);
<!-- ⬆️ returns '3' in console log/powershell -->
if you try to mix types, C# will load THE LAST WORKING FILE
If new routes are not acknowledged, it means that the newer versions are not being run
    Errors are stuck in VS Code until code is recompiled and so even fixing it may not immediately recognise fixed code
        UNTIL you hit play again

# Dictionary

Data type taking in jkey value pair (like an object, but more strictly typed)
<!-- capital 'T' in front of anything stands for "Type" - int, float, string..... -->
Dictionary<TKey, TValue>
in JS
Dictionary<string, int> codeworksCats = new Dictionary<string, int>();
codeworksCats.Add("jeremy", 7);
codeworksCats.Add("sam", 1);
codeworksCats.Add("savannah", 3);

<!-- you can make type key and name value, and vice-versa -->
Dictionary<List<string>, string> actualCats = new Dictionary<List<string>, string>();
actualCats.Add(cats, "Jeremy's");

List<string>cats = new List<string>();
cats.Add('Schnapps');
cats.Add('Marcuse');
cats.Add('Lupine');
cats.Add('9');
<!-- to remove -->
string catToRemove = cats.Find(c => c == '9');
cats.Remove(catsToRemove);


actualCats.Add(cats, "Jeremy's");
actualCats.Remove(cats);

.FindLast - starts at last w/ relevant paramenters
cats.ForEach(c => {
    Console.WriteLine(c)
})
<!-- ⬆️ this will wrtie out the names of each cat -->

#   building out a class
namespace
<!-- NOTE members are created w/ CAPITAL letters and variables/parameters LOWERCASE -->
class Cat{
    <!-- need types on all of these -->
    string Name;
    string Colour;
    int Age;
    public Cat(string name, int age, string colour) {
Age = age;
Name = name
Colour = colour
    }
}

#   code along

List<Cat> catsTheMovie = new List<Cat>();

# BCW create
    dontnet-auth
npm i -g bcw@3.3.19 <-- we are at 3.3.20, ours loaded at 3.3.16
re -fo .\name\ <--removes folder of this name


We are demo-ing in 3.3.20
    using dotnet-vue, w/o using vue(client) side, just auth(server) side


JS and Vue is front-end. C# is backend

appsetting.Development.json
    this is the env file
fileName.csproj
    this is the package.json

Program.cs is what is seen
Startup.cs - note which lines will be commented out

#   Repositories

We used Mongoose to handle repositories
    this is giving us the controls


#   Models - //some elements of schemas
Models->Cats.cs

class Cat{
    public int Id;   <-- anyone can change the value
    public string  Name;
    public string Colour;
    public readonly int Age;    <-- anyone can see it, but cannot change its value
    private bool Feisty;    <--user will have to learn by experience
    

    public Cat(int id, string name, string colour, int age, bool feisty){
        Id = id;
        Name = name;
        Colour = colour;
        Age = age;
        Feisty = feisty;
    }
}

#   Controller
CatsController.cs
<!-- data decorators/attributes affect the next definition, making our class and API CONTROLLER w/ route "...api/cats" -->
[ApiController]
[Route("api/cats")]
private readonly CatsService _service
<!-- this is a dotnet feature, not BCW ⬇️ -->
public class CatsController : ControllerBase{

<!-- how you ⬇️ append an endpoint -->
[HttpGet("test")]
public string GetTest(){   <--want anyone to access
return "hey, it worked";
}

[HttpGet]
public List<Cat> GetCats(){
     try{
    List<Cat> cats = _catsService.GetCats();
    return cats
    } catch (Exception e){
        <!-- return e;   <-- if you see arrow brackets in error message - cannot convert exception to the LIST cat -->
        
    }

}
SO
[HttpGet]
}
public ActionResult<List<Cat>> GetCats(){
     try{
    List<Cat> cats = _catsService.GetCats();
    return Ok(cats)
    } catch (Exception e){
        <!-- return e;   <-- if you see arrow brackets in error message - cannot convert exception to the LIST cat -->
    return BadRequest(e);
    }


}
<!-- [HttpGet]
GetTest(){
    try{
    
    } catch (Exception e)
}
} -->
# CatsService
private readonly CatsRepository _repo;
public class CatsService{

internal List<Cat> GetCats
}

        # Cats.cs
            namespace catRoundUp.Models;
        # CatsController
            using catRoundUp.Models;
                can use || import


files connected via namespaces and using
in Global.cs
    global using catsRoundUp.Repositories;
    global using catsRoundUp.Services;
    global using catsRoundUp.Models;


#   Repositories
CatsRepository

namespace catRoundUp.Repositories;
 public class CatsRepository{
    private List<Cat> _FakeDb;

    public CatsRepository(){

        _FakeDb = new List<Cat>();
        _FakeDb .Add(new Cat(1, "Georgie", "Orange", 5, false));
        _FakeDb .Add(new Cat(2, "Bean", "Black", 7, true));
        _FakeDb .Add(new Cat(3, "Garfield", "Orange", 100, false));
    }
 }

 internal List<Cat> GetCats()
 {
    return _FakeDb
 }

 in service

    internal List<Cat> cats = _repo.GetAllCats();
    return cats;

#   Startup.cs
ADD to Configuration of services
services.AddScoped<CatsRespository>();  <-- top to bottom, order matters
services.AddScoped<CatsService>();


Back in Model

Models->Cats.cs

class Cat{
    public int Id {get; set;}   <-- get and set the value
    public string  Name {get; set;} 
    public string Colour {get; set;} 
    public readonly int Age {get; set;}   
    public bool Feisty {get; private set;}   <--public get private set
    

    public Cat(int id, string name, string colour, int age, bool feisty){
        Id = id;
        Name = name;
        Colour = colour;
        Age = age;
        Feisty = feisty;
    }
}

Now shows up in the localhost:7045

*NOTE - No truthy or falsey in C#, just true or false

Cat cat = _repo.GetOneCatById(catId)
<!-- $ at the start allows for {} to be put ANYWHERE in the string -->
if(cat == null) throw new Exception($"no cat with that id {catId}")

#   Delete
[HttpDelete("{catId}")]
public ActionResult<string> RemoveCat(int catId){
    try{
    Cat cat = _catsService.GetOneCatById(catId)
    }catch(Exception e){
        return BadRequest(e.message)    <-- e is short for eror
    }
}


service
internal string RemoveCat(intcatId){
    Cat cat = thisGetOneCatById(catId)
    _repo.RemoveCat(catId);
    return ($"{cat.Name} has been adopted")
}

repository
internal void RemoveCat(int catId){ <-- void is 
   Cat cat = _FakeDb.Find(c => c.Id == catId);
    _FakeDb.Remove(Cat)
}
<!-- cat or integer passed, so both can be run, if the parameters were same, there WOULD be an error, but this works -->
<!-- overloading methods - same name but different parameters -->
<!-- this is good for utility parameters -->
internal void RemoveCat(Cat cat){ <-- void is 
    _FakeDb.Remove(Cat)
}

*NOTE
AddScoped vs AddSingleton
AddSingleton is created ONCE and this allows for database to truly delete items, as the original list is not redrawn


#   Create

[HttpPost]
public ActionResult<Cat> CreateCat([FromBody]Cat, catData){
    try{
    Cat cat = _catsService.CreateCat(catData)
    return Ok(cat)
    } catch(Exception e){
        return BadRequesr(e.message)
    }
}

internal Cat CreateCat(Cat catData){
    Cat cat = _repoCreateCat(catDate)
    return cat
}

internal Cat CreatCat(Cat catData){
    int catId = _FakeDb[_FakeDb.Count -1].Id;
    cataData.Id = catId + 1;
    _FakeDb.Add(catData);
    return catData;
}

#   SQL statements
dbSetup.sql
    in all the templates
        table, relational databases
    Lettercase to discriminate your and SQL's code

So in creating a new table...

CREATE TABLE hotdogs(
    <!-- using TEXT is unlimited characters -->
    <!-- MySQL words will still show in blue, but you added vs it being a method -->
    name VARCHAR(500),
    imgUrl VARCHAR(1000),
    bun VARCHAR(100),
    dog VARCHAR(100),
    hasKetchup BOOLEAN,
    hasMustard BOOLEAN,
    description VARCHAR(1000),
    expritationDate DATETIME DEFAULT CURRENT_TIMESTAMP,
    price DOUBLE

);

INSERT INTO hotdogs
<!-- expiration date skipped, so will not need value inserted -->
   ( name, imgUrl, bun, dog, hasKetchup, hasMustard, description, price)
   VALUES
   ('Huge Dog', 'url', 'Huge Toasted Whole Wheat', 'Kosher Veggie Polish', true, false, '-mungus', 45);
INSERT INTO hotdogs
<!-- expiration date skipped, so will not need value inserted -->
   ( name, imgUrl, bun, dog, hasKetchup, hasMustard, description, price)
   VALUES
   ('Danger Dog', 'url', 'Extra Spice Jalapeno', 'Extra Spicy Chorizo', false, true, 'Chorizo dog in a loaded jalapeno covered in hot mustard and horseradish', 15);
INSERT INTO hotdogs
<!-- expiration date skipped, so will not need value inserted -->
   ( name, imgUrl, bun, dog, hasKetchup, hasMustard, description, price)
   VALUES
   ('Slim Dog', 'url', 'Petite Brioche', 'Regular-sized frank', true, true, 'Pretty much a plain ol dog', 5);

<!-- * is give me all data from hotdogs, vs SELECT hasKetchup -->
<!-- * is selcect all fo the columns that exist -->
<!-- SELECT name, price, imgUrl is essentially a menu -->
SELECT * FROM hotdogs;
<!-- WHERE statement is how to filter results -->
SELECT name, price FROM hotdogs WHERE 'hasKetchup' = true;
<!-- AND filters further -->
SELECT name, price FROM hotdogs WHERE 'hasKetchup' = true AND price < 6;
<!-- LIKE is a way to search w/o knowing whole description, % are wildcard characters -->
<!-- wildcard characters allow anything t come before or after the selected characters -->
<!-- Danger% will return Danger dog, as the ending can be open -->
SELECT name, description FROM hotdogs WHERE description LIKE '%jalapeno%';

SELECT name, price FROM hotdogs ORDER BY name;
<!-- reverse order -->
SELECT name, price FROM hotdogs ORDER BY name DESC;
<!-- pagination -->
SELECT name, price FROM hotdogs LIMIT 2;
<!-- position on which the skip starts is the offset -->
SELECT name, price FROM hotdogs LIMIT 2 OFFSET 1;

*NOTE - can combine

SELECT
    name,
    price
FROM hotdogs
WHERE price < 30
ORDER BY price;

*NOTE - ORDER BY must come last

*LINK - mysqltutorial.org


right click on file and DROP - dump data
^ will need to re-execute to start up new table
Restart

CREATE TABLE hotdogs(
    <!-- using TEXT is unlimited characters -->
    <!-- MySQL words will still show in blue, but you added vs it being a method -->
    <!-- PRIMARY KEY organizes by this value -->
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(500),
    imgUrl VARCHAR(1000),
    bun VARCHAR(100),
    dog VARCHAR(100),
    hasKetchup BOOLEAN,
    hasMustard BOOLEAN,
    description VARCHAR(1000),
    expritationDate DATETIME DEFAULT CURRENT_TIMESTAMP,
    price DOUBLE

);

SELECT
    name,
    price
FROM hotdogs
WHERE price < 30
ORDER BY price;


SELECT * FROM hotdogs WHERE id = 1;
                            ^ essentially a find by id

#   remove from menu/table
<!-- affectsa all rows -->
DELETE FROM hotdogs;
<!-- tailored -->
DELETE FROM hotdogs WHERE id = 5;

DELETE FROM hotdogs ORDER BY price DESC LIMIT 1;

UPDATE hotdogs
SET price = 20
WHERE id = 1;

UPDATE hotdogs
SET price = price /2
WHERE price > 5;

TINYINT --> BIGINT is the # of # places

sgroot
n85DsI2wqb-rcp4P
SG-CodeWorks-7896-mysql-master.servers.mongodirector.com

#   GregsList C#!SECTION

CREATE TABLE cars(
    id INT  AUTO_INCREMENT PRIMARY KEY,
    make ENUM('toya', 'bww', 'goblin-car', 'egg', ) NOT NULL COMMENT "These are Mick-land model cars",
    model VARCHAR(255) NOT NULL,
    imgUrl VARCHAR(500) DEFAULT '',
    prince INT NOT NULL,
    year INT NOT NULL,
    decsription VARCHAR(1000),
    isNew BOOLEAN DEFAULT false
) default charset utf8 COMMENT '';

INSERT INTO  cars
(make, model, year, price, isNew)
VALUES
('toya', 'yoda', 1998. 4000. false);
INSERT INTO  cars
(make, model, year, price, isNew)
VALUES
('goblin-car', 'thrasher', 2000. 500. true);
INSERT INTO  cars
(make, model, year, price, isNew)
VALUES
('bww', 'subaru', 1993. 10000. false);


#   vs code is connected to database, now need appsettings.Development.json to get server hooked up

"CONNTECTION_STRING": "server=;database=; user id=; port=; password="

Model out car

namespace server.Models;

public class Car
{
    public int Id {get; set;}
    public string Make {get; set;}
    public string Model {get; set;}
    public int Year {get; set;}
    public int? Price {get; set;}   <--? makes it "null"-able
    public bool IsNew {get; set;}
    public string Description {get; set;}
    public string ImgUrl {get; set;}
}

CTRL + click to add new CarsController


namespace server.Controllers;
 [ApiController]
 [Route("api/[controller]")]

 public class CarsController : ControllerBase

private readonly CarsService carsService;

public CarsController(CarsService carsService)
{_carsService = carsService}

 [HttpGet]
 public ActionResult<List<Car>>

 Create Service
 service will need a PRIVATE READONLY repository
 use _repo

 Create Repository
 needs a database

 {private readonly IDbConnection _db;   <-- I is interface
 _db = db
 }

 in Startup.cs
*NOTE - Idb dependency is already added, is above the account services
 services.AddScoped<CarsRepository>()
 services.AddScoped<CarsService>()

 in get
 List<Car> cars
 return Ok(cars)    <-- controller
 
 In repository
 internal List<Car> GetAllCars()
 {
    string sql = "SELECT * FROM cars;"; <--semicolon for SQL & for C#
    List<Car> cars = _db.Query<Car>(sql).ToList();
    return cars;
 }

 for a single car

 [Http("{carId}")]

 public ActionResult<Car> GeCarById(){
    try{
        Car car = _carsServiceGetCarById(carId);
        return Ok(car)
    }
    catch(Execption e){
        return BadRequest(e.Message)
    }
 }

 service
 internal Car GetCarById(int carId)
 Car car = _reop.GetCaById
 if(car == null) throw new Exception($"no car w/ id{carId}")
 return car

repository
 internal Car GetCarById(int CarId)
 {
    string sql = "SELECT * FROM cars WHERE id = {carId};";"
    Car car = _db/Quert<Car>(sql).FirstOrDefault();
    return car;
}
BUT
# NOTE - do not pass strings as sql strings, need to sanitize inputs, or else lose all data. SO....
repository
 internal Car GetCarById(int CarId)
 {
    string sql = "SELECT * FROM cars WHERE id = @carId;";"
    <!-- NOTE to avoid SQL injection attacks (drop tables) -->
    <!-- pass a {key:value} into Query to match and pull valies from -->
    <!-- example {carId: 2} matches @carId and reads -->
    Car car = _db/Quert<Car>(sql, new {carId}).FirstOrDefault();
    return car;
}

[HttpPost]
 public ActionResult<Car> CreateCar([FromBody] Car carData){
    try{
        Car car = _carsService.CreateCar(carData);
        return Ok(car)
    }
    catch(Execption e){
        return BadRequest(e.Message)
    }
 }

 internal Car CreateCare(Car carData)
 Car car = _reop.CreateCar(Car carData)
 if(car == null) throw new Exception($"no car w/ id{carId}")
 return car

  internal Car CreateCar(Car carData)
 {
    string sql = @"
    INSTER INTO cars
    (make, model, year, ImgUrl, price, description, isNew)
    VALUES
    (@make, @model, @year, @ImgUrl, @price, @description, @isNew);
    ";
    Car car = _db.Query<Car>(sql, carData).FirstOrDefault();
    return car;
}

*NOTE - can test stuff in dbSetu before taking into actual files - if it works in one palce it will work in the other(throws no obvious errors)

#   Deleting

[HttpDelete]
 public ActionResult<Car> RemoveCar([FromBody] Car carData){
    try{
        Car car = _carsService.RemoveCar(carData);
        return Ok(car)
    }
    catch(Execption e){
        return BadRequest(e.Message)
    }
 }
SERVICE
 internal Car RemoveCare(Car carData)
 Car car = this.GetCarById(carId)
 <!-- this is where you would check for ownership, next -->
 _repo.removear(carId);
 return $"{car.Make} {car.Model} was remvoed from database";
REPOSITORY
  internal Car RemoveCar(int carId)
 {
    string sql = "DELETE FROM cars WHERE id = @carId";
    <!-- paranoid coder, add limit -->
    string sql = "DELETE FROM cars WHERE id = @carId LIMIT 1";
    int rowsAffected = _db.Execute(sql, new {carId});
    <!-- we are not looking for anything, so no query -->


    *NOTE - checks for paranoid people - which happens after deleting from production enviro
    if(rowsAffected > 1) throw new Exception("Get the Sr dev, I just deleted it all")
    if(rowsAffected < 1) throw new Exception("womehow nothign was deleted")


    return car;
}

#   Edit/PUT

[HttpPut("{carId}")]
public ActionResult<Car> UpdateCar(int carId, [FromBody]Car updateData){
    try{
        updateData.Id = carId
        Car car = _carsService.UpdateCar(updateData);
        return Ok(car);
    } catch(Execption e){

    }
}

internal Car UpdateCare(Car updateData)
 Car original = this.GetCarById(updateData.Id)
 <!-- no truthy falsey in C# -->
 original.Make = updateData.Make !=null ? updateData.Make : original.Make
 original.Model = updateData.Model !=null ? updateData.Model : original.Model
 original.Year = updateData.Year !=0 ? updateData.Year : original.Year
 original.Price = updateData.Price !=null ? updateData.Price : original.Price
 <!-- ^change d in model -->
 original.ImgUrl = updateData.ImgUrl ?? original.ImgUrl
 original.description = updateData.description ?? original.description

 Car car = _repo.Updatear(original);

 return car;

 REPOSITORY
  internal Car RemoveCar(Car carData)
 {
    string sql = @"
    UPDATE cars 
    SET
    make = @make,
    model = @model,
    year = @year,
    price = @price,
    imgUrl = @imgUrl,
    description = @description,
    isNew = @isNew,
    WHERE id = @id;
    SELECT * FROM cars WHERE id = @id;
    ";
    Car car = _db.Query<Car>(sql, carData).FirstOrDefault();
    return car;
 }

 #  Sam's C# Post-It lecture
 dotnet-vue
    Similar to node js express vue
SERVER
    appsettings.Developmetn.json
        CONNECTION_STRING
    C# pancakes
        bottom of screen connection check to your DB
*NOTE - CLIENT
    env.js = put same auth info in here, too!
        base URL needs to be out of https://localhost:7045
        *NOTE - client is still on 8080, it is server that has changed
    
#        dbSetup.sql - to make tables
Make accounts and album tables BOTH

Create TABLE IF NOT EXISTS albums(
    all the data in here will be based off of UML
    strings are VARCHAR
   *NOTE - TINYINT is ones and zeros, can be || BOOLEAN
    archived TINYINT DEFAULT 0,  <-- starts false
    creatorId VARCHAR (255) NOT NULL,
    FOREIGN KEY (creatorId) REFERENCES accounts(id),
)
*NOTE - format on paste could throw in spaces between parts or URL (Ctrl+D to highlight and delete all)
WHAT IF ACCOUNT GETS DELETED?

Create TABLE IF NOT EXISTS albums(
    ...
    ...
    ...                                             {    ⬇️          }
    FOREIGN KEY (creatorId) REFERENCES accounts(id) ON DELETE CASCADE,
)

combine tables by account
SELECT * FROM albums JOIN accounts;

*NOTE - break into multiple lines for clarity
*NOTE - alias out data
SELECT
FROM albums alb
JOIN accounts act ON act.id = alb.creatorId;

SELECT alb.*, act.name
FROM albums alb
    JOIN accounts act ON act.id = alb.creatorId
    WHERE id=2;

OR

SELECT alb.*, act.name
FROM albums alb
    JOIN accounts act ON act.id = alb.creatorId
    WHERE title = 'Pong';
                    ^ respect the VARCHAR, treat as string
                    canNOT % because it isn't a LIKE



SELECT
FROM accounts act
JOIN albums alb ON alb.creatorId = act.id
WHERE id = ''

#   To the files - SERVER
C# Model - build out album
    All the elements w/ the {get; set;}
*NOTE - due to dependencies, work backwards and make REPOSITORY 1ST
    Repository, Service, Controller

Bring in private readonly IDbConnection _db;
                                        ^CTRL+. to add method

Startup.cs --> register dependencies
    services.AddScoped<AlbumsRepository>();
    services.AddScoped<AlbumsService>();

    *NOTE - singleton is to be used across the entire app
    scoped creates a new instance per method

NOW can make [Http] functions
try-catches (no snippet, sadness), return

#   GET - Back to using Postman...jk, using Swagger

need to run a JOIN to get more than creatorId back <-- ie, get whole object
    add to model:
        public Account Creator {get; set;}
            property is an instance of account class
                NO MORE VIRTUALS
        in repository

    internal List<Album> Get()
    {
        string sql = @"
        SELECT
        *
        FROM albums alb
        JOIN accounts act ON act.id = alb.creatorId
        ;";
            List<Album> albums = _db.Query<Album>(sql).ToList();
            return albums
    }
Needs more specificity

    internal List<Album> Get()
    {
        string sql = @"
        SELECT
        act.*,
        alb.*
        FROM albums alb
        JOIN accounts act ON act.id = alb.creatorId
        ;";
                                     Banana words for query, order matters ⬇️
                                            ⬇️table ⬇️ table ⬇️ list item
            List<Album> albums = _db.Query<Album, Account, Album>(sql, (album, account)=>
            {
            album.Creator = account;
            return album;
            }).ToList();
            return albums
    }

#   Create - Postman should work now if you so choose
Utilize breakpoints to see what's up
    Postman catches extra details, can throw in bearer tokens
        How to get User Id --> bring in Auth
            (do not trust user to provide you id)
                Use bearer token to verify via Auth0 to get info of user who sent request

<!--*NOTE -  all C# ASYNC is accompanied by TASK -->
<!--*NOTE -  creates a new thread for async req to run in and ends thread w/ return promised -->
In controller
[HttpPost]
    public async Task<ActionResult<Album>> Create([FromBody]Album albumData)
    {
    try
    {
        Account userIngo = _auth0.GetUserInfoAsync<Account>(HttpContext);
        albumData.CreatorId = userInfo.Id;
        Album newAlbum = _albumsService.Create(albumData);
        return newAlbum;
    }catch (Exception e)
    {
        return BadRequest(e.Message);
    }
    }

    repo
    Needs more specificity, again

    internal Album Create(Album albumData)
    {
        string sql = @"
INSERT INTO albums
(title, category, coverImg, creatorID)
VALUES
(@title, @category, @coverImg, @creatorID)

        SELECT
        act.*,
        alb.*
        FROM albums alb
        JOIN accounts act ON act.id = alb.creatorId
        WHERE alb.id = LAS_INSERT_ID
        ;";
                                     Banana words for query, order matters ⬇️
                                            ⬇️table ⬇️ table ⬇️ list item
            Album newAlbum = _db.Query<Account, Album, Album>(sql, (account, album)=>
            {
            album.Creator = account;
            return album;
            }, albumData).FirstOrDefault();
            return newAlbum;
    }

*NOTE - [Authorize] <-- locks down function to authorized only
    Can put above an [HttpPost] to prohibit posting new items w/o sign-in auth

For GetById()<-- pass in the frame for id as the argument == (int albumId)

can minimize code by using regular Get() from the GetAll, but passing in the albumId as the argument

in repo, though

internal Album Get(int albumId)
{
    string sql = @"
    SELECT
    alb.*,
    act.*
    FROM albums alb
    JOIN accounts act ON alb.creatorId = act.id
    WHERE alb.id = @albumId
    ;";
    Album foundAlbum = _db.Query<Album, Account, Album>(sql, (album, account)=>
    {
        album.Creator = account;
        return album;
    }, new {albumId}).FirstOrDefault();  <-- albumId passed as object {}
    return foundAlbum 
}

#   Soft Delete
// an edit
CONTROLLER

[Authorized]
[HttpDelete("{albumId}")]    <--type of endpoint to reach
public async Task<ActionResult<Album>> ArchieveAlbum(int albumId)
{
    try{
        Account userInfo = await _ath0.GetUserAsync<Account>(HttpContext);
    Album album = _albumsService.ArchiveAlbum(albumId, userInfo.id);
    }catch(Exemption e){
        return BadRequent(e.Message)
    }
}

SERVICE
<!-- user account info is always a string, all other tables will have IDs as INT -->
<!-- this is an Auth0 thing, the way they operate -->
internal Album ArchiveAlbum(int albumId, string userId)
{
    Album album = this.Get(albumId);
    if(album.CreatorId != userId)throw new Exception("Unauthorized");
    album.Archived = !album.Archived;

    _repo.Edit(album);
}

REPOSITORY


internal void Edit(Album album)
{
    string sql = @"
    UPDATE albums
    SET
    title = @title,
    category = @category,
    coverImg = @coverImg,
    archived = @archived
    WHERE id = @id
    ;";
    _db.Execute(sql, album);
}

#   Adding pictures - data in TEST file, haha

CREATE TABLE IF NOT EXISTS pictures(
  id INT NOT NULL AUTO_INCREMENT PRIMARY KEY
   createdAt DATETIME DEFAULT CURRENT_TIMESTAMP COMMENT 'Time Created',
  updatedAt DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Last Update',
  imgUrl VARCHAR(500) NOT NULL,
  creatorId VARCHAR(255) NOT NULL,
  albumId VARCHAR(255) NOT NULL,
  FOREIGN KEY (creatorId) REFERENCES accounts(id),
  FOREIGN KEY (albumId) REFERENCES albums(id),
);

INSERT INTO pictures (imgUrl, creatorId, albumId)
VALUES("","","");

DROP TABLE pictures;    <--all w/in a table is dropped, no specification...ALL dropped
DELETE FROM albums WHERE id = 3;


#   Getting pictures in an album
USE Postman AS ROADMAP, will set endpoints

[HttpGet("{albumId}/pictures")]
    public ActionResult<List<Pictures>> GetPicturesByAlbumId(int albumId)
{
try{
    List<Picture> pictures = _picturesService
}
}

*NOTE - a service must always go through their respective repository
*NOTE - a service CAN talk to another service
*NOTE - a controller can add a private readonly and constructor to get to another service

IN REPO - only want pics from a certain album

internal List<Picture> GetPicutreByAlbumId(int albumID)
{
    string sql = @"
    SELECT
    pic.*,  <--add
    act.*  <--add
    FROM pictures
    JOIN accounts act ON act.id = pic.creatorId  <--add
    WHERE albumId = @albumId
    ;";                                             ⬇️added⬇️
    List<Picture> pictures = _db.Query<Picture, Account, Picture>(sql, (picture, account) => {  <-- this bracket piece added
        picture.Creator = account;
        return picture
    } new {albumId}).ToList();
    return pictures;
}

#   Many-to-many
Albums to accounts --> Collaborators

serves as entrypoint to database that stores IDs pointing to different tables(places)
    there is nothing to select *from* collaborators that you can get *returned*
        foreign keys are stored, nothing else - the queries go to the respective parties

CREATE TABLE IF NOT EXISTS collaborators(
    id INT NOT NULL AUTO_INCREMENT PRIMARY KEY
      createdAt DATETIME DEFAULT CURRENT_TIMESTAMP COMMENT 'Time Created',
  updatedAt DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Last Update',
  albumId INT NOT NULL,
accountId VARCHAR(255) NOT NULL,
  FOREIGN KEY (albumId) REFERENCES albums(id),
  FOREIGN KEY (accountId) REFERENCES accounts(id),
) default charset utf8 COMMENT '';

Make in order: Model, repo, service, controller


*REVIEW - _db.Query returns whole rows
    Execute.Scalar returns a single cell
        the cross-section containing the parameters we want
Creating a collaboration = adding to an instance of the model

in the accounts model

public class AccountCollaboratorViewModel : Account
{
    public int CollaboratorId {get; set}
}
⬆️ need for getting collab by album
collab repository will be responsible for getting collaborators by album
    which means accessing the collaborators service

mimic in albums

public class AlbumCollaboratorViewModel : Album <--: = "extends"
{
    public int CollaboratorId {get;set;}
    public string AccountId {get; set}
}
    ⬆️ this one will go through the account controllerl
        remember [Authorize]
        [HttpGet("collaborators")]  <-- do NOT put a slash before
    trycatch here
        going into the collaborators repository
            which is ONLY ACCESSED by collaborators service
                so must direct into collaborators service

for DELETES
    make sure there is authorization - you cannot delete other's stuff

#   Week 11 fullstack build - InstaCult

Spin up server ASAP
    make sure appsettings and env are working

    UML - many to many
        {   Repository item }
        ⬇️       ⬇️       ⬇️
        ACCT     CULT ⬅️--MEMBER
        |
        --------------------⬆️
    Build out models based on UML

dsSetup.sql - make tables est off of models


#   in repos

string sql = @"
SELECT
*
FROM cults
;";
List<Cult> cults = _db.Query<Cult>(sql).ToList();
return cults;

Get leader of cult? ⬇️

SELECT
*
FROM cults
JOIN accounts ON accounts.id = cults.leaderId
;";
List<Cult> cults = _db.Query<Cult, Account, Cult>(sql(cult, leader)=>
cult.leader = leader;
return cult;
).ToList();
return cults

Tid <-- "type ID"
    allows data tyoes to be passed down despite differing parameters
        You can cast down, not up, so REPO params can stay same

#   InstaCult front end

router, note authGuard middleware
    just checks if login is valid, so you cannot access certain pages
#   InstaCult

be sure to add the computed elements and refs where appropriate on the page

#   NOTE - InstaCult file tips
Cult and CultMember file sets
Use your CTRL + . to reduce typing when initializing files
Also to CTRL click into created method in different file

Make table to align w/ MODEL
    be mindful of foreign key
#   InstaCult - Model info
Cultist Model has Profile, Account, and Cultist
    Profile extends repo item,
    Account extends Profile
    Cultist ectends Profile

#   InstaCult - More on members
Cult controller will need access to the CultMember service, throw into the initial method

The "map" function is the between brackets section running
....(sql, (cultMember, cultist)=>
{
    cultist.CultMemverId = ciltMember.id;
    cultist.CultId = cultMember.CultId;
    return cultist;
}, new{cultist}).ToList();
return cultists


can join any table in database by just adding a join line in the repository

All async are Tasks
All Authorized routes are therefore w/in Tasks

#   InstaCult - Only leader can eject a member

Who made the cult --> only they can remove
make sure you have a null-check so that you can only delete/remove from what is there

In controller, can throw references to other existing methods
    ie this.GetCultMemberById(cultMemberId)
        Make sure there is an exception so non-leader cannot remove someone

*NOTE - Reduce member count upon member deletion

#   NOTE - InstaCult
YOU CAN UPDATE INFO DIRECTLY FROM THE TABLE
#   InstaCult - FRONT END/CLIENT

Set certain data as onMounted --> show up with page load
*NOTE - REMEMBER - to get info into AppState

*REVIEW - Account model has main constructor and an extention built in

*REVIEW - make sure your imports go through so methods are read appropriately

Pre-populate
ASYNC resetForm()
    can default info into it
        based on latest input, or set details(i.e. fee cannot be changed)

*REVIEW - many-to-many tables are just mailmen, do not have an internal set of data to return itself, just delivers to other tables.
    *Never returns own data, just other's*

#   Sam's Help Reviews App
Account is many to many w/ reports and restaurants
Front end LODELS be sure to have both ACCOUNT and PROFILE

#   Back-end Interfaces
namespace HelpReviews.Interfaces
*NOTE - <!-- "T" is for TYPE, ie Tid == type ID, standing in for stuff like INT or string -->
public interface IRepository<T, Tid>;
{
    List<T> Get();

    T GetById(Tid id);
    T Create(T newData);
    public int Update(T updateData);
    public int Delete(Tid id);

}
*ANCHOR - NOW  make restaurant repository
*ANCHOR - do not write logic in the interface
*ANCHOR - JS does not support interfaces, it will get it in next uodate, typescript has it, now

namespace HelpReviews.Repositories;
using HelpReviews.Interfaces;

public class RestaurantRepository : IRespository<Restaurant, int>       <--choose Implement option for blueprint to load (all the methods listed in interface load up)

*NOTE - do not use interface for service layer

#   SERVICE, CONTROLLER

roll out repo initiation in S, dependencies in C

  [Authorize]
    [HttpPost]

    public async Task<ActionResult<Restaurant>> CreateRestaurant([FromBody] Restaurant restaurantData)
    {
        try
        {
            Account userInfo = await _auth0.GetUserInfoAsync<Account>(HttpContext);
            restaurantData.CreatorId = userInfo.Id;
            Restaurant newRestaurant = _restaurantsService.CreateRestaurant<Account>(restaurantData);
            return newPicture;
        }
        catch (Exception e)
        {
            return BadRequest(e.Message);
        };
    }


internal Restaurant CreateRestaurant(Restaurant restaurantData)
    {
        return _repo.Create(restaurantData);
    }

in repo

string sql = @"
INSERT INTO restaurants
(name, imgUrl, description, creatorId)
VALUES
(@name, @imgUrl, @description, @creatorId);

SELECT
r.*,
a.*
FROM restaurants r
JOIN accoutns a ON a.id = r.creatorId
WHERE r.id = LAST_INSERT_ID()
;";
<!-- DAPPER statement -->
Restaurant newRestaurant = _db.Query<Restaurant, Profile, Restaurant>(sql,(restaurant, profile)=>
{
    restaurant.Creator = profile;
    return restaurant;
}, newData).FirstOrDefault();
return newRestaurant;



*account has e-mail, so use profile
<!-- (was
SELECT
FROM restaurants
WHERE id = LAST_INSERT_ID()) -->
#   DON'T FORGET THE startup file
Need to have repo and service in the file in order to process anything in the app related to it
*NOTE - do not use base64 images! Too big

*   Get functions need to be mindful of endpoints

#NOTE - be sure to specify if in the WHERE r.id = @id <-- two IDs are being passed, need to specify which one is to be used

#   Edit restaurant to shut it down set as a PUT
Place authorization so that restaurant creator is the one who can shut the restaurant down has auth

parameters for edit are Restaurant's update data(vs original), restaurant's ID, and User's ID

original.Name = Update.Name ?? original.Name
...and so on and so forth
    Mind the Bools, check Model to make amendable to this format

#   FRONT END - homepage, restaurant card
*   create restaurant service - gotta get some data
getRestaurants(){
    const res = await api.get('api.resrtaurants'
    logger.log("getting restaurants"))
}

set as onMounted on the homepage
Flesh out Client side models
*NOTE - accounts extend profiles, but we are leaving them in separate pages (I do not think InstaCult has it that way)
    ^remember the super()
        export class Account extends Profile {
            constructor(data){
                super()
                route()
            }
        }
            This can be plugged into the Restaurant model
ALL this needs to go into APPSTATE
in return, put computed roperties that will show up in template area

Move to own component AFTER demo in homepage

div -- container-fluid
    section -- row
    div -- col-4    <--this is the line for the v-for
        div -- elevation 5
        img
        div -- p3
            span
            p
        div -- d-flex justify-contnet-around
            span -- mdi
            span -- mdi

This will eventually be, from the p-3 down, in a new place
    <RestaurantCard :restaurant="r"/> will be the insert
        NEEDS PROPS
        then bind

        propsL{
            restaurant:{type: Restaurant, required:true}
        }

#   View alteration
    how to get to show specific info for specific users

    Back to server

    in service
        set a second line of logic to return only restaurants that are open, unless the shut restaurants are made by the account

    This will error out because original get request did not have an Auth
    ALSO add the elvis operator, because the return can be null on all the view if not a creator