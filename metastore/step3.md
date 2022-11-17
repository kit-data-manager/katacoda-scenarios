After registering our first metadata schema, we are now ready for doing the same
for our first metadata document. Also here, we need two inputs, which are:

1. A document's metadata record containing basic administrative metadata.
2. The metadata document itself.

The metadata record is slightly different from the one for the metadata schema, but
before explaining the mandatory properties, let's first view the metadata record:

```bash
cat metadata-record.json
```{{exec}}

There are three main properties to note here:

* `relatedResource` refers to the resource the metadata relates to. It helps you to find all metadata
documents associated with a certain resource, either identified by a
custom identifier (if using identifierType `INTERNAL`) are by URL (if using identifierType `URL`), 
depending on how your data is organized/accessible. However, MetaStore won't check what is behind
`relatedResource` but it will enforce, that there is only one metadata document of a certain schema for
each `relatedResource`.

* `schema` refers to the schema the metadata document complies to. Typically, the schema identifier is
of type `INTERNAL` telling MetaStore, that a schema for the provided identifier is available in the 
same instance. However, also `URL` is supported as `identifierType` and may point to another MetaStore
instance holding the particular schema. 

* `schemaVersion` identifies a specific version of the selected schema. For our tutorial, we did not apply
any update to the schema we've created. Thus, the schema version is still 1.

In this tutorial, we also assign the `id` property in order to be able to retrieve the document later on.
However, if you omit this property, an internal UUID will be assigned automatically by MetaStore.

After creating or obtaining a metadata record, we now get the metadata document which we want to upload. One is already available in `/usr/local/bin/metadata-document.json`. We can view it with:

```bash
cat metadata-document.json
```{{exec}}

That's it, our first metadata document is uploaded, and should comply with the schema we registered before.  
We can check this by simply seeing if MetaStore accepts our inputs by sending a POST request to the metadata repository
endpoint of MetaStore:

```bash
curl --location --request POST 'http://localhost:8040/api/v1/metadata/' --form 'record=@metadata-record.json' --form 'document=@metadata-document.json' |json_pp
```{{exec}}

If this shows our metadata documents, then everything is correctly uploaded, and adherent to the schema we defined in the previous step.

You now have the steps to set up your own instance of MetaStore. For installation instructions, view the [MetaStore Documentation](https://kit-data-manager.github.io/webpage/metastore/index.html), which also includes information on many other features of the MetaStore which aren't covered in this tutorial.