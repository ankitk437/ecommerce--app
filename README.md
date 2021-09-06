# ecommerce--app
A web app for the management of books, users and the Issue and Return of Books in a library.
User Permissions
Student

A student can

    register himself on the app
    view and edit his profile
    change his password
    search for books and view availabilty
    view his issue history

Admin

An admin can

    view and edit his profile
    search for books and view availability
    view, Edit or Delete existing books
    add new books
    issue a book to a student
    return a book issued earlier
    view all stats of the library
    view issue log and the profile of all the students
    view the profile of all admins

A note to the viewers

    You can try logging in as an admin by entering the following credentials:

    username: Director
    password: 123pass

    You can also register yourself as a student and then login to view the options available to a student.

View live App

Hosted at https://lib-manage.herokuapp.com/
Tech Stack Used
The MERN Stack

    MongoDB - Document database - to store data as JSON
    Express.js - Back-end web application framework running on top of Node.js
    React - Front-end web app framework used
    Node.js - JavaScript runtime environment

Middleware

    Redux - For flux architecture, and fetching rapidly data
    Mongoose - ODM for MongoDB

Steps followed to setup the project
Setting up server and database

    Initialise a package.json file by entering the following command in terminal, after getting into the project directory :

npm init

    Install npm packages required for backend side :

npm i express body-parser mongoose concurrently
npm i -D nodemon

    Create a file server.js to make use of the express packages

    Modify the package.json by adding the following scripts to it :

  "start": "node server.js",
  "server": "nodemon server.js",

    Create an account on MongoDB cloud Atlas, thereafter, creating a database on it and get your MongoURI exported from a file keys.js in a folder config

    Modify server.js to get connected to the database, using the MongoURI and also add the following lines at the end of server.js :

const port = process.env.PORT || 5000;
app.listen(port, ()=> console.log(`Server started running on port ${port}`));

    Type the following command to get your server running on your localhost and ensure hot-reloading, when the server-side code is modified :

npm run server

    Make Schemas for various collections to be stored in database and export them from a folder models and the REST APIs for various routes in the folder routes. Change the server.js accordingly to make the use of these REST APIs. Ensure that the APIs are working correctly, by making requests using POSTMAN

    Add JWT token based authentication and 'cors' module and use them in server.js.

Setting up the React client

    Create a folder 'client' in the project directory. Ensure that you have create-react-app CLI installed. Enter the following commands in terminal :

cd client
create-react-app .
cd ..

    In the package.json of the server, add the following scripts :

"client-install": "npm install --prefix client",
"client": "npm start --prefix client",
"dev": "concurrently \"npm run server\" \"npm run client\" ",

    Remove all the additional default setup from client folder like logo, index.css, etc. Then, configure the client to make use of bootstrap and reactstrap to make the app responsive by using following commands in terminal :

cd client
npm i bootstrap reactstrap react-popper font-awesome bootstrap-social

Add the following line to index.js :

import 'bootstrap/dist/css/bootstrap.min.css

    Install Redux for maintaining the state :

npm i redux react-redux redux-thunk

    Create a redux store, the various actions and reducers required in a folder named redux. Make corresponding changes in the React components to map the actions and state to props

Deployment

    Add the following lines to server.js :

// Serve static assets if in production
if (process.env.NODE_ENV === 'production') {
    // Set static folder
    app.use(express.static('client/build'));
  
    app.get('*', (req, res) => {
      res.sendFile(path.resolve(__dirname, 'client', 'build', 'index.html'));
    });
  }

    Add the following script to the package.json of server

    "heroku-postbuild": "NPM_CONFIG_PRODUCTION=false npm install --prefix client && npm run build --prefix client"

    Install Heroku CLI and make sure you have intialised a git repository in the project directory. Enter the following commands in the terminal :

heroku login
heroku create
git add .
git commit -am "Deployed to Heroku"
git push heroku master

    Open your heroku account and click on Open App option in the dashboard.

