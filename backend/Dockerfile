FROM node:13-alpine


WORKDIR /backend
ENV MONGODB_URI="mongodb://yolo-mongodb:27017"

COPY ./package.json .

RUN npm install && curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.35.2/install.sh | bash && nvm install 18.18.0

COPY . .

EXPOSE 5000

CMD ["npm", "start"]