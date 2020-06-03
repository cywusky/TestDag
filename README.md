# TestDag
### Using Airflow to Orchestrate Data Transformation on AWS


The following diagram illustrates the architecture of using Airflow to orchestrate data Transformation on AWS.

![This is a test image](/airflow_v3.png)

### Tempalte Codes:
The example template files include as follows.
1. Dockerfile: example Dockerfile
1. hello_world.py: example python file
1. docker_ecs_ecr_template.py: template file to perform Airflow tasks. This allows data transformation performed on AWS. A Docker image is built on EC2, then pushed to ECR. Finally, a Docker container is run on ECS, using Fargate.


### How to Use the Template Codes and Run on Airflow:
1. Push your codes to AirflowDags repo
1. Launch Airflow UI
1. Find your DAG through Airflow UI. Turn on the DAG, and trigger to run your DAG.
