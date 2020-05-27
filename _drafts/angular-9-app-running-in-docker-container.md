---
title: Angular 9 App Running In Docker Container
excerpt: Learn to build and host your Angular app running in a docker container!
header:
  teaser: ''
categories:
- Software Development
tags:
- Nginx
- Docker
- Angular 9
comments: false

---

### Create an angular app

    npm install -g @angular/cli
    ng new my-amazing-app
    cd my-amazing-app
    ng serve

### Build the app

    ng build --prod

### Configure Dockerfile

1. Add `Dockerfile` (no extension) to the root of your angular app
2. Add the following into the docker file

   _(replace 'your-amazing-app' with your app name.)_

    FROM node:13.3.0 AS compile-image
    
    WORKDIR /opt/ng
    COPY package.json ./
    RUN npm install
    
    ENV PATH="./node_modules/.bin:$PATH"
    
    COPY . ./
    RUN ng build --prod
    
    FROM nginx
    COPY --from=compile-image /opt/ng/dist/your-amazing-app /usr/share/nginx/html