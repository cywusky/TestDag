# AirflowDAGs
This repository automatically syncs with the Airflow instance running on AWS every minute on the master branch.

## Architecture
The following diagram illustrates the architecture of using Airflow to orchestrate data transformation on AWS.


![System diagram for using Airflow on AWS](/image/airflow_v4.png)


## Example Template Files
The example template files include the three parts\. 
* **Dockerfile**: an example Dockerfile.
* **hello_world.py**: an example Python file, which acts as data transformation file.
* **docker_ecs_ecr_template.py**: a template file to perform Airflow tasks. This allows data transformation performed on AWS.<br>
This tempalte file will allow the follwing processes:

A Docker image is built on EC2, then pushed to ECR. Finally, a Docker container is run on ECS, using Fargate. You will need to revise the following args for your use.

``` 
task_id: a task ID is used in Airflow
default_docker_args: a dictionary to define input arguments
dagName: DAG name is used in Airflow. This is what you will see on Airflow UI.
```

For more information about the input args to registera an ECS task, 
[input args from AWS](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/ecs.html#ECS.Client.register_task_definition)
[input args from AWS]
(https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/ecr.html)

## How to Use the Template Codes and Run on Airflow
1. Create your own ```Dockerfile```
1. Create your own template file based on  ```docker_ecs_ecr_template.py```
1. Push your codes for data transformation, Dockerfile, and the revised template file to AirflowDags repo. 
1. Verify all of your newly pushed codes exist on EC2 under the following folder ``` ~/airflow/dags/AirflowDags ```.
1. Launch [Airflow UI](https://fst-apc-airflow.agro.services/admin/).
1. Find your DAG through Airflow UI. Turn on the DAG, and trigger to run your DAG.
