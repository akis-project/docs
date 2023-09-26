# Running Locally 💻

Ensure that you have the followings installed before you attempt to run the project in your computer:

| [Docker ](https://www.docker.com/) | 24.0.4, build 3713ee1 |
| ---------------------------------- | --------------------- |

- Note that the reason why docker is used in local development is because of volume bindings.

## Steps

1. Create a folder named `akis-project` somewhere in your computer.
2. Clone repositories from github
   - [akis-react-app](https://github.com/akis-project/akis-react-app)
   - [akis-nodejs-api](https://github.com/akis-project/akis-nodejs-api)
   - [akis-flask-api](https://github.com/akis-project/akis-flask-api)
   - [docker-compose](https://github.com/akis-project/docker-compose)
3. Switch to respective branches of each repository and pull the latest code:

```sh
# akis-react-app
git switch dev

# akis-nodejs-api
git switch dev

# akis-flask-api
git switch dev

# docker-compose
# stay in 'main'
```

4. Create volumes in project directory (you must be in akis-project folder, at the root)

!!! Warning
Because we are binding local volumes to docker containers, we need to create those volumes manually in the host machine.

This part is a MUST!

!!!

Run the following commands to create directories of volumes:

```sh
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
mv .env.dev .env
mv docker-compose.dev.yml docker-compose.yml

# To see logs:
docker compose up

# To run in detached mode:
# docker compose up -d
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
