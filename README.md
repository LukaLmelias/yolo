# Usage

This project can be run in two methods:
-   Docker
-   Manual set-up


## Running using Docker:
The only requirement in order to run using docker is of course docker which can be installed following this [instructions](https://docs.docker.com/engine/install/)


Once docker is installed; follow the following steps to start the app
- 1 git clone this repo

```
git clone git@github.com:LukaLmelias/yolo.git
```

- 2 Enter into yolo (the created directory)

```
cd yolo
```

- 3 Start-up the app using docker compose

```
docker compose up 
```


If everything went well, you should be able to acess the app on:   http://localhost:3000

## Instructions on Manual set-up:

### Requirements
Make sure that you have the following installed:
- [node](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-18-04) 
- npm 
- [MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/) and start the mongodb service with `sudo service mongod start`

## Navigate to the Client Folder 
 `cd client`

## Run the folllowing command to install the dependencies 
 `npm install`

## Run the folllowing to start the app
 `npm start`

## Open a new terminal and run the same commands in the backend folder
 `cd ../backend`

 `npm install`

 `npm start`

 ### Go ahead a nd add a product (note that the price field only takes a numeric input)
