# simple-express-rest-crud-sample
☕ Simple REST application made with express.js

### Run the sample locally
```bash
# clone the repository locally
git clone https://github.com/estebanborai/simple-express-rest-crud-sample.git

# install dependencies
cd simple-express-rest-crud-sample/server/
yarn

# run the server
yarn start

# open your browser at the following URL
# http://localhost:4200/api/palette
```

### Run using Docker
```bash
# build Docker assets
docker-compose up --build
```

### Build an run MongoDB
```bash
# step into simple-express-rest-crud-sample/database/
# build docker image and add the tag "simple-express-rest-crud-sample-database"
docker build -t simple-express-rest-crud-sample-database .

# run docker container with the recently builded image
docker run --net=host -p 27017:27017 simple-express-rest-crud-sample-database
```

### Use local MongoDB instance
This project supports a local MongoDB instance.
To use a MongoDB connection hosted by your system and not in Docker, you must set the MODE environment
variable in `.env` file to "DEV" as follows:

```
// server/.env
MODE=DEV
SERVER_PORT=4200
USE_DATABASE=true
MONGO_DB_PORT=27017
MONGO_DB_DATABASE=simple-express-rest-crud-sample
MONGO_DB_USERNAME=admin
MONGO_DB_PASSWORD=admin
```

This setting will attempt to connect to a MongoDB instance with the following URL:
`mongodb://localhost:${MONGO_DB_PORT}/${MONGO_DB_DATABASE}`

> The following environment variables must never change as docker-compose uses those values
> for the connection to the database.
> MONGO_DB_DATABASE, MONGO_DB_USERNAME, MONGO_DB_PASSWORD

### SSH into Docker container
There is a docker exec command that can be used to connect to a container that is already running.

```bash
docker exec -it <container id> /bin/bash
```

Get the docker <container id> using `docker container ls` in your terminal, copy the *CONTAINER ID* and change it for *<container id>* in the command above.

### Debugging
Theres two ways to debug this application:
  - Locally
  - Docker

##### Locally
Here are some steps to setup the environment in order to debug this application using VSCode and Nodemon.
This project already has the configuration loaded at: `.vscode/launch.json`.
All you have to do is:

1. Run the project using **debug** script as follows `yarn run debug`
2. Open Visual Studio Code in the Debug section
3. Select the **Node: Nodemon** option from the select menu right to the **DEBUG** title.
4. Click on the "Play" button
5. Choose the option that says "--inspect" from the prompt menu
6. Set your breakpoints and have fun debbuging!

[Reference](https://github.com/Microsoft/vscode-recipes/tree/master/nodemon).

##### Docker
Use the *docker-compose.debug.yml* file instead *docker-compose.yml* to setup the environment.
```bash
docker-compose -f docker-compose.debug.yml up --build
```

This command will gather Docker images and build them using the configuration defined in the *docker-compose.debug.yml* file.

When Docker is done, you will be able to attach to the process using either Google Chrome Devtools or Visual Studio Code.

- Google Chrome Devtools:
Open Google Chrome in the following URL: `chrome://inspect/#devices`.
Click on `inspect`, in the list of severs behind the options, this will open a new window
with Chrome Devtools in the context of your app.

A breakpoint in the first line of `app.js` will be active for the moment you open the "Sources" tab.

- Visual Studio Code
Step into the Debug tab in your Visual Studio Code instance.
Select "Node: Docker Debug" option from the list in the top.
Finally, click the "start" icon.

### Required VSCode Extensions
1. ESLint
2. EditorConfig for VSCode
