# Get-Programming-with-Node.js

.load messages.js load a file in repl

To exit your Node.js REPL environment, you can type .exit, press Ctrl-C twice, or press Ctrl-D twice.
The exports object is a property of the module object. module is both the name of the code files in Node.js and one of its global objects. exports is shorthand for module .exports.

npm publish	Saves and uploads a package you build to the npm package community
npm start	Runs your Node.js application (provided that the package.json file is set up to use this command)
npm stop	Quits the running application

You also see a package-lock.json file created at the root level of your project directory. This file is automatically created and used by npm to keep track of your package installations and to better manage the state and history of your project’s dependencies. You shouldn’t alter the contents of this file.


Luckily, the request listens for a specific data event. req.on(“data”) is triggered when data is received for a specific request.

example of webserver isong http module :-

```const routeResponseMap = {                              1
  "/info": "<h1>Info Page</h1>",
  "/contact": "<h1>Contact Us</h1>",
  "/about": "<h1>Learn More About Us.</h1>",
  "/hello": "<h1>Say hello by emailing us here</h1>",
  "/error": "<h1>Sorry the page you are looking for is not here.</h1>"
};

const port = 3000,
  http = require("http"),
  httpStatus = require("http-status-codes"),
  app = http.createServer((req, res) => {
    res.writeHead(200, {
      "Content-Type": "text/html"
    });
    if (routeResponseMap[req.url]) {                    2
      res.end(routeResponseMap[req.url]);
    } else {
      res.end("<h1>Welcome!</h1>");                     3
    }
  });

app.listen(port);
console.log(`The server has started and is listening on port number:
 ${port}`);
 ```

Create a controllers folder within your project folder.
Create a homeController.js file within controllers.
Require your home controller file into your application by adding the following to the top of main.js:
const homeController = require("./controllers/homeController");
Move your route callback functions to the home controller, and add them to that module’s exports object. Your route to respond with a vegetable parameter, for example, can move to your home controller to look like listing 9.6. In homeController.js, you assign exports.sendReqParam to the callback function. sendReqParam is a variable name, so you can choose your own name that describes the function.
Listing 9.6. Moving a callback to homeController.js
```
exports.sendReqParam = (req, res) => {              1
  let veg = req.params.vegetable;
  res.send(`This is the page for ${veg}`);
};
```
1 Create a function to handle route-specific requests.
Back in main.js, change the route to look like the next listing. When a request is made to this path, the function assigned to sendReqParam in the home controller is run.
Listing 9.7. Replacing a callback with a controller function in main.js
```
app.get("/items/:vegetable", homeController.sendReqParam);     1
```
Handle GET requests to “/items/:vegetable”.
Apply this structure to the rest of your routes, and continue to use the controller modules to store the routes’ callback function. You can move your request-logging middleware to a function in the home controller referenced as logRequestPaths, for example.
Restart your Node.js application, and see that the routes still work. With this setup, your Express.js application is taking on a new form with MVC in mind.



http :-
createServer 


Request,Response =>
response.WriteHead()
response.write()
.end()


Request
.method
.url
.header


ReadableStream 


fs-module

readFile
existsSync

cookie-parser and express-session module


Expressjs
app.get()
set() --> to set configs app.set("port", process.env.PORT || 3000) // all vars used by app can be set here
app.listen()
.post , .get


req - to allow params and body use :- you add express.json and express.urlencoded to your app instance to analyze incoming request bodies. Notice the use of req.body to log posted data to the console in listing 9.5. 
params
body, body.vegetable
```
app.get("/items/:vegetable", (req, res) => {        1
  let veg = req.params.vegetable;
  res.send(`This is the page for ${veg}`);
});
```

url
query


res
send()
render()

express-generator package ca be used to generate some bare none code

for templating , we could use ejs , handlebar.js

<%= %>

can be used in templating engine with ejs
As long as you continue to add your views to the views folder and use EJS, your application will know what to do.


passing params from controller to view 

```
exports.respondWithName = (req, res) => {
  let paramsName = req.params.myName;               
  res.render("index", { name: paramsName });         
};
```

steps to add layout :- 
```
const layouts = require("express-ejs-layouts");      1

app.set("view engine", "ejs");                       2
app.use(layouts);
```
install express-ejs-layouts for layouts
app.use(layouts) 
Next, create a layout.ejs file in your views folder

use catch all route as error

add a middleware to app
```
exports.logErrors = (error, req, res, next) => {      1
  console.error(error.stack);                         2
  next(error);                                        3
};
```

call
```
logErrors
```

app structure
.                                 1
|____main.js
|____public
| |____css
| | |____confetti_cuisine.css
| | |____bootstrap.css
| |____images
| | |____product.jpg
| | |____graph.png
| | |____cat.jpg
| | |____people.jpg
| |____js
| | |____confettiCuisine.js
|____package-lock.json
|____package.json
|____controllers
| |____homeController.js
| |____errorController.js
|____views
| |____index.ejs
| |____courses.ejs
| |____contact.ejs
| |____error.ejs
| |____thanks.ejs
| |____layout.ejs




using mongodb:-

```
 await client.connect();
    console.log('Connected successfully to server');
    const db = client.db(dbName);
    const collection = db.collection('movie');
    return collection
```

```
collection.count({id:movie.id}))
collection.insertOne(movie)
collection.find().limit(5)
collection.updateOnce();

```


adding models :-

```
const subscriberSchema = mongoose.Schema({     1
  name: String,                                2
  email: String,
  zipCode: Number
});

```


```
var subscriber1 = new Subscriber({
  name: "Jon Wexler",
  email: "jon@jonwexler.com"
}); 
```

```
subscriber1.save((error, savedDocument) => {     2
  if (error) console.log(error);                 3
  console.log(savedDocument);                    4
});


```

Run a Qry
```
Subscriber.findOne({
    name: "Jon Wexler"
  })
  .where("email", /wexler/);
myQuery.exec((error, data) => {
  if (data) console.log(data.name);
});                     

```

How ot connect to controller and main app\
```
app.get("/contact", subscribersController.getSubscriptionPage);   1
app.post("/subscribe", subscribersController.saveSubscriber);    
```

in `getSubscriptionPage`  use this code

```
exports.getSubscriptionPage = (req, res) => {     1
  res.render("contact");
};

exports.saveSubscriber = (req, res) => {          2
  let newSubscriber = new Subscriber({
    name: req.body.name,
    email: req.body.email,
    zipCode: req.body.zipCode
  });                                             3

  newSubscriber.save((error, result) => {         4
    if (error) res.send(error);
    res.render("thanks");
  });
};

```


```
Subscriber.deleteMany()
  .exec()                                     2
  .then(() => {
    console.log("Subscriber data is empty!");
  });

```

delete many 

schema vaalidations

```
const subscriberSchema = new mongoose.Schema({
  name: {                                       1
    type: String,
    required: true
  },
  email: {                                      2
    type: String,
    required: true,
    lowercase: true,
    unique: true
  },
  zipCode: {                                   3
    type: Number,
    min: [10000, "Zip code too short"], //error like this
    max: 99999
  }
});

```


mongooes queries :
find
findone
findById
remove({}) will remove all 

we can build complex types like this 

```

const mongoose = require("mongoose"),
  {Schema} = mongoose,

  userSchema = new Schema({                                  1
  name: {                                                    2
    first: {
      type: String,
      trim: true
    },
    last: {
      type: String,
      trim: true
    }
  },
  email: {
    type: String,
    required: true,
    lowercase: true,
    unique: true
  },
  zipCode: {
    type: Number,
    min: [1000, "Zip code too short"],
    max: 99999
  },
  password: {
    type: String,
    required: true
  },                                                         3
  courses: [{type: Schema.Types.ObjectId, ref: "Course"}],   4 //complex type
  subscribedAccount: {type: Schema.Types.ObjectId, ref:
 "Subscriber"}                                            5
}, {
  timestamps: true                                           6
});

```

use https://transform.tools/json-to-mongoose to build schema

Flash messages are semipermanent data used to display information to users of an application. These messages originate in your application server and travel to your users’ browsers as part of a session. Sessions contain data about the most recent interaction between a user and the application, such as the current logged-in user, length of time before a page times out, or messages intended to be displayed once.


session based authentication : -

```
const expressSession = require("express-session"),      1
  cookieParser = require("cookie-parser"),
  connectFlash = require("connect-flash");
router.use(cookieParser("secret_passcode"));            2
router.use(expressSession({
  secret: "secret_passcode",
  cookie: {
    maxAge: 4000000
  },
  resave: false,
  saveUninitialized: false
}));                                                    3
router.use(connectFlash());   

```

The flash is a special area of the session used for storing messages. Messages are written to the flash and cleared after being displayed to the user. The flash is typically used in combination with redirects, ensuring that the message is available to the next page that is to be rendered.

route.get('route' , niddleware)

hashing password

 bcrypt.hash(user.password, 10).then(hash => {                    2
    user.password = hash;
    next();
  })
  
  
  use passport.js for auth instead of manually doing
  
  
  install packages like :-
  passport
  passport-local-mongoose -S 
  
  to use passport.js use
  
 ```
const passport = require("passport");
router.use(passport.initialize());
router.use(passport.session());   
```
then 

```
const User = require("./models/user");                  1
passport.use(User.createStrategy());                    2
passport.serializeUser(User.serializeUser());           3
passport.deserializeUser(User.deserializeUser());
  ```
  
  ```
  const passportLocalMongoose = require("passport-local-mongoose")
  ```
  
  main code :-
  
  ```
  passport.authenticate("local", {     1
  failureRedirect: "/users/login",                 2
  failureFlash: "Failed to login.",
  successRedirect: "/",
  successFlash: "Logged in!"
}),
  ```


to return json instead of view use res.json() instead of res.render()

if user is signed send jwt from API
```
apiAuthenticate: (req, res, next) => {                          1
  passport.authenticate("local",(errors, user) => {
    if (user) {
      let signedToken = jsonWebToken.sign(                      2
        {
          data: user._id,
          exp: new Date().setDate(new Date().getDate() + 1)
        },
        "secret_encoding_passphrase"
      );
      res.json({
        success: true,
        token: signedToken                                      3
      });
    } else
      res.json({
        success: false,
        message: "Could not authenticate user."                 4
      });
  })(req, res, next);
}
```
