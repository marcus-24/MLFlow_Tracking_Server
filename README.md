# MLFlow_Tracking_Server

## Objective

The purpose of this repository is to create an cloud agnostic MLFlow server to keep track of machine learning operations (MLOPs) in a shared location. This service is also dependent on a PostgreSQL database to store the MLFlow metadata (run name, model input parameters, etc.) of each run and MinIO (AWS S3 alternative) to store ML Artifacts (model pickle files, environment.yml, etc.).

## Required software

- https://docs.docker.com/get-started/get-docker/
- https://docs.docker.com/compose/install/

## Starting the service

The services required are created in its designated docker containers. Before running the docker compose file, you will need to update the configurations in the `config.env` to add connection parameters for PostgreSQL, MinIO and MLflow.

Once the `config.env` has been updated, you can test the containers locally running the following command in your terminal:

`docker-compose --env-file config.env up -d --build`
