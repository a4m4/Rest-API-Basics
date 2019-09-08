# Rest-API-Basics
Basics of Rest APIs


Rest APIs are just about data, no ui logics is exchanged.
Rest APIs are just node servers which expose different endpoints(http method + path) for clients to send requests to.
JSON is the most common data format used for both req and res.
Rest APIs are decoupled from the clients that use them, they dont share any connection history or store any connection history.
REST apis doesnt store connection history.

Attach data in JSON format and let other end know by setting the "content-type" header.
CORS(Cross-origin-resource-shairing) error occur when using an API that doesnot set CORS header.
 CORS can be done by following function :
          app.use((req,res,next) => {
            
            res.setHeader('Access-Control-Allow-Origin', '*');   //allows access to any client
            res.setHeader('Access-Control-Allow-Methods', 'GET,POST,PUT,DELETE');  //define methods like post get put delete or all by *
            res.setHeader('Access-Control-Allow-Headers', 'Content-Type', 'Authorization');  // or you can use * for all
            
            });
