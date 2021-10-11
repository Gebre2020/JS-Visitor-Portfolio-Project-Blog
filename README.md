
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
    - `rails new IS-Vistor-Project-Backend --api--database=postgresgl`
    - cd JS-visitor-project-backend 
    - code. 
Next I created a github repository and upload the application to git hub. Then in the 
terminal I run 
    - git add. 
    - git commit-m "start project" 
    - git push 
    - & copy from the github 3 lines (git remote..., git branch, git push ...) 
      paste and run to the terminal. 
Then to check refresh the github. 

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
I use a resource generate to the database migration and run the parent element first 
    - rails and resource location name 
    - rails and resource trip name address budget float location belongs to  
    - rails db:create 
    - rails db: migrate  
I write a data in the seed file then run  
    - rails db:seed. 
Then check the data run`rails console` and he relationship of the table. 
Next go to the 'config' folder then, open the 'initializers' folder and open 'corse.rb' file 
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

For the frontend I run ` mkdir JS-Visitor-Project-Frontend ` and run
    - cd JS-Visitor-Project-Frontend
    - code . in the terminal.
In the editor I create a folder & file of image, src, index.html, index.js, README.md
and style.css. Also, in the src folder I create location_service.js, location.js, 
trip_service.js and trips.js.
  - Then writing html code to the index.html file and in the body & adding the script src 
    link to connect the javascript files. 
  - Next, I have to check the index.js file connection to my application page by writing 
    ' console.log('Hello') ' in the index.js file and run `open index.html` in the terminal
    to open the app browser. And inspet the page and open the console check Hello printed.

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
  - In the trip_servive.js write a getTrip() function with fetch request.

    getTrips() {
        fetch(this.port + `/trips`)
        .then(response => response.json())
        .then(json => console.log(json)
    }

In order to print/see the object, the console I have add/call by writing 
    tripCall.getTrips()
    locationCall.getLocations()
at index.js file.





