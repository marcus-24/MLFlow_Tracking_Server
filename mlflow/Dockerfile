# syntax=docker/dockerfile:1

# use slim version of python to reduce container size
FROM python:3.10-slim 

# update linux software packages and install curl
RUN apt-get update && apt-get install -y curl

# install files for pip
COPY ./mlflow/requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

EXPOSE 5000