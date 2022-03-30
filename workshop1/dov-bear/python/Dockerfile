ARG PY_VER=3.11.0a6-slim-buster

FROM python:${PY_VER}

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

RUN pip3 install -r requirements.txt

HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \ 
CMD curl -s -f http://localhost:${APP_PORT}/ready > /dev/null || exit 1 

#RUN npm ci

#run stage
#ENV APP_PORT=4000
#for documentation to see which ports are exposed
#EXPOSE ${APP_PORT} 

CMD [ "python3", "main.py" ]
#CMD [ "gunicorn", "-b", "--host=0.0.0.0", "--port=3000" ]
#"$APP_PORT"