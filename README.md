# AirflowDAGs
This repository automatically syncs with the Airflow instance running on AWS every minute on the master branch.

##  Using Airflow to Orchestrate Data Transformation on AWS.
The following diagram illustrates the architecture of using Airflow to orchestrate data transformation on AWS.


![System diagram for using Airflow on AWS](/image/airflow_v6.png)


## Run HelloWorld Example Files
The example files include the three parts\. 
##### 1. Dockerfile: an example Dockerfile.
##### 2. hello_world.py: an example Python file, which acts as a data transformation code.
##### 3. docker_ecs_ecr_template.py: a template file to execute Airflow tasks, which enables data transformation performed on AWS. <br> 

Airflow on EC2 will orchestrate the follwoing processes: A Docker image is built on EC2, then pushed to ECR. Finally, a Docker container is run on ECS, using Fargate. You will need to revise the following input arguments for your own use. 


``` 
- task_id: a task ID is used in Airflow <br>
- default_docker_args: a dictionary to define input arguments for tasks on ECR, ECS <br>
- dagName: DAG name is used in Airflow. This is what you will see on Airflow UI.
```

[Mroe information about the input arguments to register an ECS task using boto3](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/ecs.html#ECS.Client.register_task_definition)

Check more information about how to use input arguments to [register an ECS task using boto3]. (https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/ecs.html#ECS.Client.register_task_definition).


## How to Use the Template Codes and Run on Airflow
1. Create a ```Dockerfile```
1. Create a revised template file based on  ```docker_ecs_ecr_template.py```
1. Push the codes for data transformation, Dockerfile, and the revised template file to AirflowDags repo. 
1. Verify all of your newly pushed codes exist on EC2 under the following folder ``` ~/airflow/dags/AirflowDags ```.
1. Launch [Airflow UI](https://fst-apc-airflow.agro.services/admin/).
1. Find your DAG through Airflow UI. Turn on the DAG, and trigger to run your DAG.
