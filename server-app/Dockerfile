FROM node:20-alpine
WORKDIR /usr/src/app
COPY package.json package.json
COPY app.js app.js
RUN npm install
ENTRYPOINT [ "node", "app.js" ]
