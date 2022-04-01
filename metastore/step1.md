At first, create an instance of MetaStore by running docker 

`docker run -d -p 8040:8040 kitdm/metastore:latest`{{execute}}

---

**NOTE**
It may take a while until the service has started. If you receive an error in the next execution step, please try again after a couple of seconds.

---

After startup, MetaStore offers two main endpoints: one for accessing the schema registry (/api/v1/schemas) 
and one for accessing the metadata repository (/api/v1/metadata).

For listing all registered metadata schemas we can use the following 'curl' command:
 
`curl http://localhost:8040/api/v1/schemas/ --header 'Accept: application/json' |json_pp`{{execute}}

As expected, an empty result set is returned. The same is the case for listing all metadata records via

`curl http://localhost:8040/api/v1/metadata/ --header 'Accept: application/json' |json_pp`{{execute}}

The same result can be obtained by using the basic graphical frontend offered by MetaStore, which is 
accessible via http://localhost:8040/dashboard. In the course of this tutorial we'll continue 
focussing on accessing MetaStore via RESTful endpoints.
