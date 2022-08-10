After registering our first metadata schema, we are now ready for doing the same
for our first metadata document. Also here, we need two inputs, which are:

1. A document's metadata record containing basic administrative metadata.
2. The metadata document.

The metadata record is slightly different from the one for the metadata schema, but
before explaining the mandatory properties, let's first create the metadata record:

```bash
cat << EOF > metadata-record.json
{
    "id":"my_first_document",
    "relatedResource": {
        "identifier": "anyResourceId",
        "identifierType": "INTERNAL"
    },
    "schema": {
        "identifier": "my_first_schema",
        "identifierType": "INTERNAL"
    },
    "schemaVersion": 1
}
EOF
```{{exec}}

There are three main properties: 

`relatedResource` refers to the resource the metadata relates to. It helps you to find all metadata
documents associated with a certain resource, either identified by a
custom identifier (if using identifierType `INTERNAL`) are by URL (if using identifierType `URL`), 
depending on how your data is organized/accessible. However, MetaStore won't check what is behind
`relatedResource` but it will enforce, that there is only one metadata document of a certain schema for
each `relatedResource`.

`schema` refers to the schema the metadata document complies to. Typically, the schema identifier is
of type `INTERNAL` telling MetaStore, that a schema for the provided identifier is available in the 
same instance. However, also `URL` is supported as `identifierType` and may point to another MetaStore
instance holding the particular schema. 

`schemaVersion` identifies a specific version of the selected schema. For our tutorial, we did not apply
any update to the schema we've created. Thus, the schema version is still 1.

For our tutorial, we also assign the `id` property in order to be able to retrieve the document later on. 
However, if you omit this property, an internal UUID will be assigned by MetaStore.

After having a metadata record, we now create a metadata document which we want to upload:

```bash
cat << EOF > metadata-document.json
{
"givenName": "John",
"familyName": "Doe",
"age": 42
}
EOF
```{{exec}}

That's it, our first metadata document which should comply with the schema we registered before.  
Let's check, if MetaStore accepts our inputs by sending a POST request to the metadata repository
endpoint of MetaStore:

```bash
curl --location --request POST 'http://localhost:8040/api/v1/metadata/' --form 'record=@metadata-record.json' --form 'document=@metadata-document.json' |json_pp
```{{exec}}