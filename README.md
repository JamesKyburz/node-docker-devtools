# node-docker-devtools

![Docker Image CI](https://github.com/JamesKyburz/node-docker-devtools/workflows/Docker%20Image%20CI/badge.svg)

## How to use this image

### Create a `Dockerfile`

```dockerfile
FROM jameskyburz/node:12.16.1-alpine3.11-devtools as devtools

WORKDIR /usr/src/app

COPY package.json package-lock*.json npm-shrinkwrap*.json /usr/src/app/
RUN npm i

FROM node:12.16.1-alpine3.11

WORKDIR /usr/src/app

COPY . .
COPY --from=devtools /usr/src/app/node_modules /usr/src/app/node_modules

USER node

ENTRYPOINT ["node", "src/index"]
CMD []
```
# license
[Apache License, Version 2.0](LICENSE)
