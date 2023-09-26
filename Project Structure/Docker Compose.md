---
order: 4
---

This is the main component :brain: that orchestrates the other components.

It does the followings:

1. Stores config files
2. Manages services
3. Manages volumes
4. Manages networks
5. Manages environment variables

There is a `docker-compose.yml` file that defines the services, volumes and networks of the project.

However, because we have a live version running in a `vpa-com16` server, we have two versions of `docker-compose.yml` file.
The services and environment variables will differ in two versions.

1. `docker-compose.dev.yml`
   - To run the project locally.
   - Because we don't have a standalone server for development, this version can also be used for local development.
2. `docker-compose.prod.yml`:
   - To run the project in a server.
   - Currently `vpa-com16` is running that version.

If you compare two files, they will look like this:
![test](/static/two-versions.png)

!!! info
Notice the `akis-proxy` service. It is only used in the production version. We don't use in the development version or in the local machine.
!!!

Now let's see the definition of each component in details and how they work together. :point_right:
