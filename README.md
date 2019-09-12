# Rest-API-Basics
Basics of Rest APIs


Rest APIs are just about data, no ui logics is exchanged.
Rest APIs are just node servers which expose different endpoints(http method + path) for clients to send requests to.
JSON is the most common data format used for both req and res.
Rest APIs are decoupled from the clients that use them, they dont share any connection history or store any connection history.
REST apis doesnt store connection history.

To create new Nodejs backend logics, we have to first install dependencies which are :
   1- npm install --save express
   2- npm install --save nodemon       //to add restart of server facility
   3- npm install --save body-parser   // to add routes

Then open package json file and make heading of start in scripts tag of "start : "nodemon app.js"   //any file name from where you wanna start server

For form data, we will use body-parser as : app.use(bodyParser.urlEncoded());
For json data, we will use body-parser as : app.use(bodyParser.json());




Attach data in JSON format and let other end know by setting the "content-type" header.
CORS(Cross-origin-resource-shairing) error occur when using an API that doesnot set CORS header.
 CORS can be done by following function :
          app.use((req,res,next) => {
            
            res.setHeader('Access-Control-Allow-Origin', '*');   //allows access to any client
            res.setHeader('Access-Control-Allow-Methods', 'GET,POST,PUT,DELETE');  //define methods like post get put delete or all by *
            res.setHeader('Access-Control-Allow-Headers', 'Content-Type', 'Authorization');  // or you can use * for all
            
            });


JSON.stringify() is a method that takes js object and convert it into json

For Server side validation we have to install one package i.e
   npm install --save express-validator
   then it should require in Routes file where you wanna validate like :
   const { body/check } = require('express-validator/check');  
and for use in any route :
   router.post('/post',
               [ body('title').trim.isLength({min: 5}),
                 body('content').trim.isLength({min: 5})],
               feedController.createPost);
