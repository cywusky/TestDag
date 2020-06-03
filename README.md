# TestDag
### Using Airflow to Orchestrate Data Transformation on AWS


The following diagram illustrates the architecture of using Airflow to orchestrate data Transformation on AWS.

![This is a test image](/airflow_v3.png)

### Tempalte Codes:
The example template files include as follows.
1. Dockerfile: example Dockerfile.
1. hello_world.py: example python file.
1. docker_ecs_ecr_template.py: template file to perform Airflow tasks. This allows data transformation performed on AWS. A Docker image is built on EC2, then pushed to ECR. Finally, a Docker container is run on ECS, using Fargate.


### How to Use the Template Codes and Run on Airflow:
1. Create your own Dockerfile
1. Revise docker_ecs_ecr_template.py
You will need to revise the following args for your use.
* Item 1: task_id: a task ID is used in Airflow
* Item 1: default_docker_args: a dictionary to define input args
* Item 1: dagName: DAG name is used in Airflow. This is what you will see on Airflow UI.

1. Push your codes to AirflowDags repo.
1. Launch Airflow UI.
1. Find your DAG through Airflow UI. Turn on the DAG, and trigger to run your DAG.
