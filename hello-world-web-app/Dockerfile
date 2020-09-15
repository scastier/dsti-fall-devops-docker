FROM node:12
# official node from Docker, 12 is version tag

WORKDIR /usr/src/app
# create this path in container

COPY package*.json ./
#copy this on container

RUN npm install

COPY . .

EXPOSE 8080
# port used

CMD [ "node", "server.js" ]
# cmd launched at start of container
