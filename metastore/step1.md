At first, create an instance of MetaStore by running docker 

`docker run -d -p 8040:8040 kitdm/metastore2:latest`{{execute}}

---

**NOTE**
It may take a while until the service has started. If you receive an error in the next execution step, please try again after a couple of seconds.

---

After startup, MetaStore offers two main endpoints: one for accessing the schema registry (/api/v1/schemas) 
and one for accessing the metadata repository (/api/v1/metadata).

For listing all registered metadata schemas we can use the following `curl` command:
 
```bash
curl http://localhost:8040/api/v1/schemas/ --header 'Accept: application/json' |json_pp
```{{exec}}

As expected, an empty result set is returned. Don't worry if you get the message about an empty reply, simply try again in a few seconds as it takes a minute or so for the server to catch up. Similarly, we can list all metadata records via

```bash
curl http://localhost:8040/api/v1/metadata/ --header 'Accept: application/json' |json_pp
```{{exec}}

The same result can in theory be obtained by using the basic graphical frontend offered by MetaStore, which is 
accessible via http://localhost:8040/dashboard. However, as we are working within the Killercoda environment, the localhost is unaccessible. Therefore, we'll continue focusing on accessing MetaStore via RESTful endpoints.

If you are following along with a local installation, then you should be able to access the UI with the above link.
