In order to create a new collection you need to send a POST request to the service. 
All attributes of a collection are optional, but for our example we add some of them
for illustration purposes:

`curl --location --request POST 'http://localhost:8080/api/v1/collections/' \
--header 'Content-Type: text/plain' \
--data-raw '[
    {
        "id":"test123",
    },
    "properties":{
        "ownership":"Katacoda Tutorial",
        "license": "CC-BY"
    },
   "description": "Collection containing tutorial data"
   }
]'`{{execute}}

If we now list all collections, we should receive one element containing the 
previously created collection:

`curl http://localhost:8080/api/v1/collections/`{{execute}}
