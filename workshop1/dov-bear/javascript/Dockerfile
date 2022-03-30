ARG NODE_VER=12.18.1

FROM node:${NODE_VER}

#build stage
ENV NODE_ENV=production

ARG APP_DIR=/app

#cd in APP_DIR
WORKDIR ${APP_DIR}

RUN echo 'hello'

# ADD main.js
# ADD package.json
# ADD package-lock.json
# ADD public public
# ADD views view

#copy files from host into container using .dockerignore
ADD . .

RUN npm install --production

HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \ 
CMD curl -s -f http://localhost:${APP_PORT}/ready > /dev/null || exit 1 

#RUN npm ci

#run stage
CMD [ "node", "main.js" ]