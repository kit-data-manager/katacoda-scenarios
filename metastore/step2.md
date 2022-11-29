We will now register our first metadata schema to MetaStore. Therefore, we need two inputs:

1. A schema's metadata record containing basic administrative metadata.
2. The schema itself.

For the metadata record, we have to provide two properties, which are shown in the file `schema-record.json`. We can view this file:

```bash
cd /usr/local/bin/ && cat schema-record.json
```{{exec}}

The first property is the `ID` by which the schema can be referenced later on. The second property 
states that we want to provide a JSON-type schema. `type` defines the validator which is used 
later on to validate the schema itself and its associated metadata documents.
MetaStore currently supports JSON and XML schemas.

After creating the first input, we now need the actual schema. According to our schema metadata record, 
it has to be a JSON schema. For this tutorial, we use a very simple schema even though MetaStore supports
complex schemas.

The schema we will use is already available in our filesystem with the file name `pp13-basic-schema.json`:

```
{
	"$schema": "http://json-schema.org/draft/2019-09/schema#",
	"$id": "http://www.example.org/schema/json",
	"type": "object",
	"title": "Json schema for tests",
	"default": {},
	"required": [
		"title"
	],
	"properties": {
		"title": {
			"$id": "#/properties/string",
			"type": "string",
			"title": "Title",
			"description": "Title of object."
		},
		"general": {
			"type": "object",
			"properties": {
				"software": {
					"type": "string"
				}
			}
		},
		"relatedImages": {
			"type": "array",
			"items": {
				"type": "string"
			}
		}
	},
	"additionalProperties": false
}
```

Now that we have both input files, we can use them to register our first schema in MetaStore.

To do this, we can simply send a POST request to the endpoint of the schema registry component of MetaStore via the `curl` command by pointing it to out schema record and schema files:

```bash
curl --location --request POST 'http://localhost:8040/api/v1/schemas/' --form 'record=@schema-record.json' --form 'schema=@pp13-basic-schema.json' |json_pp
```{{exec}}

The piped command `json_pp` at the end is only used to print the output in the console in a neat format ("pretty printer").

When we list schemas again, we should see our newly-registered schema with `id = 'my_first_schema'` as the result:

```bash
curl http://localhost:8040/api/v1/schemas/ |json_pp
```{{exec}}

Confirm it's correct, and let's move on to registering a metadata document.