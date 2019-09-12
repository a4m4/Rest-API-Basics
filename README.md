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

To send error when validation is not met , we have to implement some logic on server side and it is done in controllers file where :
   const { validationResult } = require('express-validator/check'); 
and for logic :
   const errors = validationResult(req);
   if(!errors.isEmpty()) {
            return res.status(422).json({ message: 'Validation failed' });
            }
            
Express works simple and the alternate of above error given by express is :   // more elegant way
   if(!errors.isEmpty()) {
         const error = new Error('Validation failed');
         error.statuscode = 422;
         throw error;
      }
      
    is hi file k end me jo catch hhoga na usme end me next(err); zarur krna hoga
    
      and by using this, at the end of routes use this function :
         app.use((error,req,res,next) => { console.log(error)
                                           const status : error.statusCode;
                                           const message : error.message;
                                           res.status(status).json({ message: message }); 
                                           });
         
            
Server side validation and client side validation are not same, they works according to their logics.


To upload images on server side db, install package on server project file:
    npm install --save multer
the go in app.js file:
    const multer = require('multer'); 
then you have to :
   const fileStorage = multer.diskStorage({
   destination : （req,file,cb）=> {
      cb(null, 'images');
               },
    filename : (req,file,cb) => {
      cb(null, new Date().toISOString() + '-' + file.originalname); 
                 }
   });
   
   for the use of this :
      app.use(
            multer({ storage : fileStorage ,  fileFilter : fileFilter }).single('image')
            );
