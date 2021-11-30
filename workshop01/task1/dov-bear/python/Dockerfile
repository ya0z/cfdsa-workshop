FROM python:3.8-slim-buster
ARG APP_DIR /app
WORKDIR ${APP_DIR}
ADD requirements.txt .
RUN pip3 install -r requirements.txt
COPY . .
