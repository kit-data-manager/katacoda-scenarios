## Setting up the Collection API Microservice

At first, create an instance of the collection-api service by running docker 

`docker run -d -p 8080:8080 kitdm/collection-api:latest`{{execute}}

---

**NOTE**
It may take a while until the service has started. If you receive in the next execution step, please try again after a couple of seconds.

---

Now, let's check how many collections we already have. This can be done via 'curl' as follows:

`curl http://localhost:8080/api/v1/collections/ |json_pp`{{execute}}

It's not very surprising, that there is no collection, yet. Our next step will be to 
create our first collection.
