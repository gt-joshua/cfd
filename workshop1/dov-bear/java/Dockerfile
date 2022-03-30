ARG JAVA_VER=16-alpine3.13

FROM openjdk:${JAVA_VER}

#build stage
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

RUN ./mvnw dependency:go-offline

HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \ 
CMD curl -s -f http://localhost:${APP_PORT}/ready > /dev/null || exit 1 

#RUN npm ci

#run stage
CMD ["./mvnw", "spring-boot:run"]