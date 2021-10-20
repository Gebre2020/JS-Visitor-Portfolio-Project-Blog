
  **  JS Visitor Portfolio Project Blog  **

As a Flatiron School student I build a Java Script with ruby on rails backend app 
called Js-Visitor-Project-Backend and Front end with JavaScript. I have to bring 
ruby on rails and JavaScript together (backed and frontend) in to one single app. 
My app is about visitor to find or create a location's place name and to input 
the trip's name, address and budget. It also manages to render all trips and location, 
to create, edit, update and delete.

First, to start the project I used two separate entities/folders backend reusable 
backend for other front end applications like an api to use over and over again.

So I create two new ones and create the backend first. In the terminal I run 
    - cd Desktop, 
    - `rails new JS-Vistor-Project-Backend --api--database=postgresgl`
    - cd JS-visitor-project-backend 
    - code. 
Next I created a github repository and upload the application to git hub. Then in the 
terminal I run 
    - git add. 
    - git commit-m "start project" 
    - git push 
    - & copy from the github 3 lines (git remote..., git branch, git push ...) 
      paste and run to the terminal. 
Then to check the github refresh the page. 

  * Backend (Ruby on Rails) Setup 

I create two models with the relationship. The first is locations with attributes of
name and has many trips. 
The second is trips with attribute of name, address, budget, location, id & belongs to location.

    class Location < ApplicationRecord
        has_many :trips
    end

    class Trip < ApplicationRecord
    belongs_to :location
    end
In order to create the model and the table, I use a resource generate and run the parent element first 
    - rails g resource location name 
    - rails g resource trip name address budget float location belongs to  
    - rails db:create 
    - rails db: migrate  
I build a data in the seed file then run  
    - rails db:seed. 
Then check the data run`rails console` and the relationship of the table. 
Next going to the 'config' folder then, open the 'initializers' folder and open 'corse.rb' file 
and uncomment from 'config middleware' up to the end. 
And, change at the 'origins example.com' code to 'origins "*"' to grab it from anywhere 
after the app development finish and allowing websites to access api and change "*" to url.

Then open Gemfile and uncomment gem 'rack-cores' and  run bundle install.
  - Next in the controller create a CRUD method render with json.
  - run 'rails server' for starting the server (this would open it by default on 
    http://localhost:3000) to check & see the connection with data object.
  - I add a serializers to the app and run `rails g serializer location` and
    `rails g serializer trip`
  - At Gemfile I add `gem 'active_model_serializers' '~> 0.10.2'`
  - `gem 'fast_jsonapi'` and run bundle install in the terminal. 

   * Front End Setup

For the frontend I run ` mkdir JS-Visitor-Project-Frontend ` at the terminal and run
    - cd JS-Visitor-Project-Frontend
    - code . in the terminal to open the visual studio code editor.
In the editor I create a folder & file of image, src, index.html, index.js, README.md
and style.css. Also, in the src folder I create location_service.js, location.js, 
trip_service.js and trips.js.
  - Then writing html code to the index.html file and in the body & adding the script src 
    link to connect the javascript files. 
  - Next, I have to check the index.js file connection to my application page by writing 
    ' console.log('Hello') ' in the index.js file and run `open index.html` in the terminal
    to open the app browser. And inspect the page and open the console check Hello printed.

Next I have to create a github respository. In the terminal run
   - git init  
   - git add .
   - git commit -m "fronted started"
   - go to a github and I create a git hub respository for frontend application & run
     ` git remote ..., git branch, git push... ` in the terminal & refresh the github.

I check the connection of backend and frontend by fetch request. I started from trip_service.js
file. creating a class method with constructor.

Inside in index.js file creating a global variable

    const port = `http://localhost:3000`;
    const tripCall = new TripService(port);
    const locationCall = new LocationService(port);

and check the connection in the terminal by tripCall & locationCall of instance method.
  - In the 'trip_servive.js' file write a getTrip() function with fetch request 

    getTrips() {
        fetch(this.port + `/trips`)
        .then(response => response.json())
        .then(json => console.log(json)
    }

In order to print/see the object,  in the page inspect console I have add/call by writing 
    tripCall.getTrips()
    locationCall.getLocations()
at 'index.js' file.

- Then in the 'tripService.js' file to get the instance method change the code
        `.then(json ==> console.log(json))` to

        `.then(json => {
           //debugger
            for(const trip of json.data) {
               let t = new Trip(trip)              
               t.attachToDom()
            }
        })`

- Next in the 'trip.js' file I build a class method with constructor takes an arrgument.
  And I create an element li assign with id and add "static all = []" and "Trip.all.push(this)
  in the class Trip & constructor method.
  Then I create a rendering function called 'render() {...}'
  Also I build a function called 'attachToDom()'

      `attachToDom() {       
        Trip.tripsContainer.appendChild(this.render())
      }`

  and at the top in the class Trip I assign 'static tripsContainer' variable.

    * Create an Object

- Next I build create function
  . 1st I have build a trip-form id inside 'index.html' file and 
    also I add location-dropdown form

       ` <form id="trip-form">           
          <label for="trip-name">Name: </label>
          <input type="text" name="name" id="trip-name"/><br/>          
          <label for="trip-address">Address: </label>
          <input type="text" name="address" id="trip-address"/><br/>          
          <label for="trip-budget">Budget: </label>
          <input type="number" name="budget" id="trip-budget" min="0" step="0.01"/><br> 
          <label for="location-dropdown">Choose a Location Name:</label>
          <select name="location_id" id="location-dropdown"></select><br/><br/>       
          <label for="location-Name">Location Name: </label>
          <input type="text" name="name" id="location-name"/><br/>          
          <input class="button" type="submit" value="Create Trip"/>        
        </form>`
  . 2nd I create an event listener function in 'index.js' file 
          `form.addEventListener('submit', handleSubmit)`
          `function handleSubmit(e) {...}` 
    And, I assign a variable for trip-form and location-dropdown in the 'index.js' file 
          `const form = document.getElementById("trip-form")`
          `const dropdown = document.getElementById("location-dropdown")`

- Next, in the 'trip-service.js' file I build a createTrips function
        `createTrips() {
            const tripInfo = {
               trip: {...}
            }          
            const configObject = {
              method: 'POST',
              header: {...},
              body: JSON.stringify(tripInfo)
            }
            fetch(...)
            .then(...)
            .then(json => {...}) 
        }` 
- Then in the 'index.js' file I assign a variable name for each value of attributes

      `const nameValue = document.getElementById("trip-name")`
      `const addressValue = document.getElementById("trip-address")`
      `const budgetValue = document.getElementById("trip-budget")`
      `const locNameValue = document.getElementById("location-name")`

- Next in the 'location.js' file build a class method with constructor takes 
  an argument attribute and assign a static location container also add

      `static all = [];`
      `static locationContainer = document.getElementById('loc-container');`
      and `Location.all.push(this) ` inside constructor .

- Then in side 'locaion-service.js' file build the class locationService 
  method with constructor and create an instance method called getLocations 
  of fetch request.
  After I created a fetch request, open 'location.js' file & create a function
  to add/render() the information & creating a new object to the location dropdown is called
  addToDrop.

      * Edit, Update, and Delete

  - Next I am going to build an edit, update & delete functions.
    . 1st I need to add a button in 'trip.js' file in render function 
      Edit Trip and Delete button.
    . Then I add an event listener in constructor attributes  
       `this.element.addEventListener('click', this.handleClick)`
    . Then I create handleClick function and UpdateTripInfo()     
       ` handleClick = e => {...}`
       ` updatedTripInfo() {...}`
      In the updateTripInfo() function I add a code to call tripCall.updateTrip(this). 
  - Next in the 'trip-service.js' file I create updateTrip(trip) function for PATCH
    request. Also I build deleteTrip(e) {...} function. 

       * Backend

  - In the backend in the 'trip-controller.rb' file I add a location_name attribute 
    in the private trip_params method then in the 'trip.rb' model file I build 
    location_name method to find or create location attribute. Then, in 'trip_serializer.rb'
    file I add :location_name at attributes in order display at front/client page when 
    I created a location_name.

  - In order Update/display the new or created location name I have to const 
    findLoc variable in fetch request at 'createTrips() function in the 
    'trip-service,js' file.  
      `const findLoc = Location.all.find(l => parseInt(l.id) === t.locationId)`


  # Code & Demo

You can check out this project on Github Backend and Frontend 
`https://github.com/Gebre2020/JS-Visitor-Project-Backend`   and
`https://github.com/Gebre2020/JS-Visitor-Project-Frontend`

see the demo at `https://www.youtube.com/watch?v=RcMxTCQd3j8` hosted

  ## License & copyright

Licensed under the [MIT License](LICENCE).

