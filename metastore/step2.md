Now, we will register our first metadata schema to MetaStore. Therefore, we need two inputs:

1. A schema's metadata record containing basic administrative metadata.
2. The schema itself.

For the metadata record, we have to provide two properties, which are shown in the file `schema-record.json`. We can view this file:

```bash
cat schema-record.json
{
  "schemaId" : "my_first_schema",
  "type" : "JSON"
}
```{{exec}}

The first property is the ID by which the schema can be used later on, the second property 
states, that we want to provide a JSON schema. The type defines the validator which is used 
later on to validate the schema itself and associated metadata documents.
Currently, JSON and XML schema types are supported.

After creating the first input, we now need the actual schema. According to our schema metadata record, 
it has to be a JSON schema. For this tutorial, we use a very simple schema even though MetaStore supports
complex schemas.

```bash
cat << EOF > metadata-schema.json
{
  "$schema": "https://json-schema.org/draft/2019-09/schema",
  "title": "Person",
  "description": "A simple person schema",
  "type": "object",
  "properties": {
    "givenName": {
      "description": "The given name of the person",
      "type": "string"
    }, 
   "familyName": {
      "description": "The family name of the person",
      "type": "string"
    }, 
   "age": {
      "description": "The (optional) age of the person",
      "type": "integer"
    }
  },
  "required": [ "givenName", "familyName" ]
}
EOF
```{{exec}}

Now, that we have both input files create, we can use them to register our first schema in MetaStore.
Therefor, we send a POST request to the endpoint of the schema registry component of MetaStore:

```bash
curl --location --request POST 'http://localhost:8040/api/v1/schemas/' --form 'record=@schema-record.json' --form 'schema=@metadata-schema.json' |json_pp
```{{exec}}

If we now list schemas, we should obtain a schema with id 'my_first_schema' as result:

```bash
curl http://localhost:8040/api/v1/schemas/ |json_pp
```{{exec}}