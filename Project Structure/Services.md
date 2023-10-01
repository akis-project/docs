---
order: 3
---

# Services

- Services are docker containers that runs applications inside. They are the main building blocks of the project.
- Each application is isolated from others, with its own operating system, dependencies, environment variables, ports, volumes, etc.

### Service definitions

+++ akis-react-app

- Serves UI
- Communicates with `akis-nodejs-api`
- Stores cookies for authentication
- Runs on port 3000 (when running in dev)
- Runs on port 3001 (when running in prod)

+++ akis-nodejs-api

- Runs express server
- Runs backend logic
- Communicates with `akis-react-app`, `akis-flask-api`, and `mongo`
- Sets cookie in the `akis-react-app` after a successful login
- Hosts images statically to `akis-react-app`
- Shares volume between `akis-flask-api`
- Runs on port 5001 (always)

+++ akis-flask-api

- Runs flask server
- Runs machine learning model
- Gets image from `akis-nodejs-api` and returns back transcription results
- Saves images and crops to local directory of host instance
- Shares volume with `akis-nodejs-api`
- Runs on port 5000 (always)

+++ mongo

- Runs NoSQL database
- Stores user information, transcription results and login sessions.
- Runs on port 27017 (always)

+++ :warning: akis-proxy (only in production) :warning:

!!!
This service is only used in production environment.
It is necessary to proxy requests from `demos.sabanciuniv.edu` to the host instance (`vpa-com16`).
Otherwise the host instance will not be able to receive requests from outside. Thus, nodejs api won't be able to set cookies in react application.
And this will lead `cross-origin cookie` errors which means you won't be able to login.
!!!

- Proxy layer between `demos.sabanciuniv.edu` and host instance (`vpa-com16`).
- Utilizes [node-http-proxy](https://www.npmjs.com/package/node-http-proxy) library
- Receives requests from `demos.sabanciuniv.edu`
- Forwards requests to host instance's 3001 (react) and 5001 (nodejs) ports
- Runs on port 3000 (when running in prod)
- Why do we need such proxying? _short answer: reverse-proxy of demos_

  - All the docker containers are designed to communicate each other using internal docker network.
  - `akis-react-app` is the frontend service, it will store session cookies on the browser
  - `akis-nodejs-api` is the backend service which stores session, i.e. it is cookie-setter of the frontend
  - And there is a _reverse-proxy_ configured in `demos.sabanciuniv.edu`'s machine, which forwards HTTPS(443) requests to `vpa-com16`'s 3000 port.
  - But by its nature, backend service is designed to set cookies in frontend, which is bundled and delivered to the client's browser.
  - So, because of this reverse-proxying of `demos.sabanciuniv.edu`, the client should be `demos.sabanciuniv.edu` instead of `vpa-com16`'s `react-app` service.
  - To achieve this api & client interaction, we a proxy service which will forwards requests from `demos.sabanciuniv.edu` to `vpa-com16`'s front and backend services.
  - In the end, backend service will assume that incoming request is actually coming from `demos` even though it is designed to receive requests from `vpa-com16`'s 3000 port. Then it will set cookies in `demos` successfully ✅
  - If we didn't have this akis-proxy service, users who visit `demos` wouldn't be able to sign-in even though their credentials were true. This is because of [cross-origin cookies](https://medium.com/@sharadokey/understanding-cors-and-cross-origin-cookies-bf36d624da78).

+++

### Service Schema

![service schema](/static/service-schema.jpg)

- Those services share volumes and networks between each other.
- In order to figure out how system works, you need to understand how each service communicates each other.

!!! info
You can find details of this flow in the [Transcription Workflow](/transcription-workflow) page.
!!!
