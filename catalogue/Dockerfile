FROM node:20.19.5-alpine3.22 AS build
WORKDIR /opt/server   
COPY package.json .
COPY *.js .
RUN npm install 

### using multi stage build to optimize the size of the image

FROM node:20.19.5-alpine3.22
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
WORKDIR /opt/server
USER roboshop
COPY --from=build /opt/server /opt/server
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
CMD ["node", "server.js"]
