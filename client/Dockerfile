FROM node:13-alpine

WORKDIR /client/

ENV PATH /client/node_modules/.bin:$PATH

COPY package.json .

RUN npm install && curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.35.2/install.sh | bash && nvm install 13.12.0

COPY . .


EXPOSE 3000

CMD ["npm", "start"]