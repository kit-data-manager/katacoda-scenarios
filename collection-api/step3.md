Great, if we now list all metadata records for the relatedResource with id `anyResourceId`, we can see the entry we've just uploaded:

`curl --location --request GET 'http://localhost:8040/api/v1/metadata/?relatedResourceId=anyResourceId' \
--header 'Accept: application/vnd.datamanager.metadata-record+json' |json_pp`{{execute}}

The same way, we can also list all metadata records associated with our schema `my_first_schema` as follows: 

`curl --location --request GET 'http://localhost:8040/api/v1/metadata/?schemaId=my_first_schema' \
--header 'Accept: application/vnd.datamanager.metadata-record+json' |json_pp`{{execute}}

It's not surprising, that we get the same result as we only have on document registered. 

If we instead want to obtain the metadata document itself, we have to use the `id` of the record as part of the request URL: 

`curl --location --request GET 'http://localhost:8040/api/v1/metadata/my_first_document' \
--header 'Accept: application/json' |json_pp`{{execute}}

