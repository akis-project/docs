---
icon: device-desktop
order: 1
---

# Running Locally

Ensure that you have the followings installed before you attempt to run the project in your computer:

| [Docker ](https://www.docker.com/) | 24.0.4, build 3713ee1 |
| ---------------------------------- | --------------------- |

- Note that the reason why docker is used in local development is because of volume bindings.

!!! info
Oh, also at least 30 GB free space :skull:
!!!

## Steps

1. Create a folder named `akis-project` somewhere in your computer.
2. Clone repositories from github
   - [akis-react-app](https://github.com/akis-project/akis-react-app)
   - [akis-nodejs-api](https://github.com/akis-project/akis-nodejs-api)
   - [akis-flask-api](https://github.com/akis-project/akis-flask-api)
   - [docker-compose](https://github.com/akis-project/docker-compose)
3. Switch to respective branches of each repository and pull the latest code, then install dependencies.

+++react

```sh
# Go into directory
cd akis-react-app

# Pull latest dev code
git switch dev
# Or you can use 'git checkout -b dev' and then 'git pull origin dev'

# Install dependencies
npm install
```

+++nodejs

```sh
# Go into directory
cd akis-nodejs-api

# Pull latest dev code
git switch dev
# Or you can use 'git checkout -b dev' and then 'git pull origin dev'

# Install dependencies
npm install
```

+++flask

```sh
# Go into directory
cd akis-flask-api

# Pull latest dev code
git switch dev
# Or you can use 'git checkout dev' and then 'git pull origin dev'

# Here we don't install dependencies.
# Because we don't know if flask has such ability that it reflects local code changes immediately to the docker container.
# React and Nodejs can do that. We don't need to restart the containers to see the changes. (At least it was working when i left the project)
```

+++

4. Create volumes in project directory (you must be in akis-project folder, at the root)

!!! Warning
Because we are binding local volumes to docker containers, we need to create those volumes manually in the host machine.

This part is a MUST!

!!!

Run the following commands to create directories of volumes:

```sh
# Make sure you are at the root of the project folder
mkdir volumes
cd volumes
mkdir db
mkdir uploads
```

After this step, make sure you have the following folder structure:
![final folder structure](/static/folder-structure.png)

6. Change environment variables

Run the following commands to change name of environment files and docker compose file:

```sh
cat .env.dev > .env
cat docker-compose.dev.yml > docker-compose.yml

```

7. Run the project

Within only one command, you can start the whole project.

```bash
docker-compose up -d
```

!!! info
The `-d` flag is for running the containers in the background.

To see the logs in interactive mode, remove the `-d` flag.
!!!
