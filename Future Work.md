---
icon: clock
order: -1
---

# Future Work

There might be some work to do in the future throughout the system. These are:

- If we cancel `demos.sabanciuniv.edu` reverse-proxying, there should be a `nginx` or `apache` configuration in `vpa-com16` and SSL certification.
- React can be served by `nginx` or `apache` using their pre-built docker images.
- Storage should be cleaned periodically for the sake of data privacy and protection. (`/uploads` volume)
- There might be some security issues in the system. These should be investigated and fixed.
- For local development, we should give up using `docker-compose`. This is because of the volume bindings. We should find a way to bind volumes in local development. Also each time shutting containers, rebuilding service images and running compose again when we change the code ==> **takes freaking time** :boom:!
- There can be a better authentication and MFA implementation.
- Users' can have tokens to transcribe images, .i.e. a new user can transcribe max 10 pages. After that, he/she should buy/request tokens to transcribe more.
