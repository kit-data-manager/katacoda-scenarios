At first, create an instance of the collection-api service by running docker 

`docker run -d -p 8080:8080 kitdm/collection-api:latest`{{execute}}

---

**NOTE**
It may take a while until the service has started. If you receive in the next execution step, please try again after a couple of seconds.

---

Now, let's check how many collections we already have. This can be done via 'curl' as follows:

`curl http://localhost:8080/api/v1/collections/ |json_pp`{{execute}}

It's not very surprising, that there is no collection, yet. In the next steps, we will describe how to build up the example defined in the documentation (url of the documentation).

The Collection API offers a graphical web frontend in order to visualize managed collections, collection items and relationships between them as well as associated metadata. To access the web frontend, you can open the following link in your browser: http://localhost:8080/static/overview.html. Currently, there is no collections to visualize.
