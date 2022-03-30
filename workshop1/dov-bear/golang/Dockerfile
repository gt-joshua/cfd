ARG GO_VER=1.17

FROM golang:${GO_VER} AS builder

#build stage
ARG APP_DIR=/app

#cd in APP_DIR
WORKDIR ${APP_DIR}

#RUN echo 'hello'

# ADD main.js
# ADD package.json
# ADD package-lock.json
# ADD public public
# ADD views view

ADD main.go .
ADD go.mod .
ADD go.sum .

## 1st container to compile
RUN go build -o main main.go

#####################################################

## 2nd container to run
FROM golang:${GO_VER}

#build stage
ARG APP_DIR=/app

#cd in APP_DIR
WORKDIR ${APP_DIR}

COPY --from=builder ${APP_DIR}/main .
ADD public public
ADD templates templates

ENV APP_PORT=3000 INSTANCE_NAME="dov-go-bear"

HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \ 
CMD curl -s -f http://localhost:${APP_PORT}/ready > /dev/null || exit 1 

#run stage
EXPOSE ${APP_PORT}

ENTRYPOINT [ "./main" ]