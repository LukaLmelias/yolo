FROM node:13-alpine


WORKDIR /backend
ENV MONGODB_URI="mongodb://mongodb:27017"

COPY ./package.json .

#RUN apk update && apk upgrade && apk add curl

RUN npm install 
#&& curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.35.2/install.sh | bash && nvm install 18.18.0

COPY . .

EXPOSE 5000

CMD ["npm", "start"]