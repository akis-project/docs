# Environment Variables

All environment varibles of services are provided by `docker-compose.yml` file.

!!! info
`docker.compose.yml` also get variables from `.env` file
!!!

### List of Environment Variables in `.env` and Where They Are Used

+++ Prod
| Variable | Description | react-app | nodejs-api | flask-api | mongodb | proxy |
| -------- | :----------- | :----: | :----: | :----: | :----: | :----: |
| NODE_ENV | Determines `production` or `development` environment | ✅ |✅ | | | |
| DOCKER_EXTERNAL_IP | Value of Host machine's IP address. `localhost` or `127.0.0.1` in development. vpa-com16's IP address in production | ✅| ✅ | ✅ | | |
| MONGODB_DATABASE_NAME | mongodb database name| |✅| | ✅ | |
| MONGODB_ROOT_USERNAME | mongodb root username | | | | ✅ | |
| MONGODB_ROOT_PASSWORD | mongodb root password | | | | ✅ | |
| MONGODB_NODEJS_USERNAME | mongodb username for connecting nodejs | | ✅ | | ✅ | |
| MONGODB_NODEJS_PASSWORD | mongodb password for connecting nodejs | | ✅ | | ✅ | |
| SESSION_SECRET | session secret of nodejs | |✅ | | | |
| REACT_APP_PORT | port on which react is running | ✅ | ✅ | | | ✅ |
| NODEJS_API_PORT | port on which nodejs is running | ✅ | ✅ | ✅ | | ✅ |
| FLASK_API_PORT | port on which flask is running | | | ✅ | | |
| MONGODB_PORT | port on which mongodb is running | | | | ✅ | |
| REVERSE_PROXY_HOST :warning: | `https://demos.sabanciuniv.edu` currently... | ✅ | ✅ | | | ✅ |
| PROXY_PORT :warning: | port on which proxy service is running | | | | | ✅ |
+++ Dev
Everything is same except `REVERSE_PROXY_HOST` is `PROXY_PORT`. Those are only used in production.
+++
