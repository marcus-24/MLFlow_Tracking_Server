# MLFlow_Tracking_Server

## Objective

This repository aims to create a cloud-agnostic MLFlow server to track machine learning operations (MLOPs) in a shared location. This service is also dependent on a PostgreSQL database to store the MLFlow metadata (run name, model input parameters, etc.) of each run and MinIO (an AWS S3 alternative) to store ML Artifacts (model pickle files, environment.yml, etc.).

## Required software

- https://docs.docker.com/get-started/get-docker/
- https://docs.docker.com/compose/install/
- https://docs.anaconda.com/miniconda/install/

## Starting the service

The required services are created in their designated docker containers. Before running the docker-compose file, you will need to update the configurations in the `config.env` to add connection parameters for PostgreSQL, MinIO, and MLflow (except the MINIO_ACCESS_KEY and MINIO_SECRET_ACCESS_KEY variables. More on this later).

Once the `config.env` has been updated, you can test the containers locally by running the following command in your terminal:

`docker-compose --env-file config.env up -d --build`

With the services running, log into the Minio service in your browser using the http://localhost:<MINIO_PORT> and the username and password that you set in the MINIO_ROOT_USER and MINIO_ROOT_PASSWORD variables. After a successful login, click the Access Keys option within the toolbar on the left of the screen and select Create Access Key. Copy and paste the Access Key and Secret Key into your MINIO_ACCESS_KEY and MINIO_SECRET_ACCESS_KEY variables within your config.env file respectively. Then click the Create button to save the key.

Now we will have to restart the services with this new setting to enable the create bucket service to create the default MLFlow bucket with the new key settings. To restart the service, first shutdown the running containers using:

`docker-compose down`

Then rebuild the containers:

`docker-compose --env-file config.env up -d --build`

Now you have a fully running MLFlow server that you can save experiment parameters and artifacts within the http://localhost:<MLFLOW_PORT>

## Testing MLFlow server in Python

You can test this new service using the example.py script included in this repository. The example script runs scikit learn's standard example of logistic regression with the model being tracked by the mlflow server that was created. First, you need to install the Python environment using the command below in the repository root directory (make sure you have Miniconda installed on your computer):

`conda env create -f environment.yml`

Then activate this new environment using:

`conda activate mlflow_example`

You can now run the code with (make sure the MLFlow server is running in the background or this code will fail):

`python example.py`
