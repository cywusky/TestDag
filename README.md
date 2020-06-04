# AirflowDAGs
This repository automatically syncs with the Airflow instance running on AWS every minute on the master branch.

##  Using Airflow to Orchestrate Data Transformation on AWS.
The following diagram illustrates the architecture of using Airflow to orchestrate data transformation on AWS.


![System diagram for using Airflow on AWS](/image/airflow_v6.png)


## Hello World Example
### The Hello World Example Files
1. Dockerfile: an example Dockerfile.
2. hello_world.py: an example Python file, which acts as a data transformation code.
3. docker_ecs_ecr_template.py: a template file to execute Airflow tasks, which enables data transformation performed on AWS. 

Airflow on EC2 will orchestrate the following processes: A Docker image is built on EC2, then pushed to ECR. Finally, a Docker container is run on ECS, using Fargate. See the diagram above for more details. <br> 


### Run Hello World Example
1. Launch [Airflow UI](https://fst-apc-airflow.agro.services/admin/).
1. Click ```DAGs``` on the menu bar.
1. Choose ``` dcoker_ecs_ecr_template_demo ```
1. Turn ```On``` button for ``` dcoker_ecs_ecr_template_demo ```. Then click ```Trigger DAG```.
1. Choose ```Graph View``` to monitor the 3 subprocesses in a DAG.
1. From AWS console, you can verify whether a Docker image is pushed to ECR, and whether an ECS task is created and run.

* Go to ECR: check if the Repository ``` fst-airflow/dev/demo ``` exists.
* Click ``` fst-airflow/dev/demo ``` repository, verify if a Docker image exists.
* Go to ECS: under Task Definitions, choose ```airflow``` and verify if a new task is created.
* Go to ECS: choose ```Clusters```. Choose ```fargate``` cluster.
* Click ```Tasks``` tab, select a Task with its Task Definition starting with ```airflow```. You can select that task and moinotor its status.

## How to Use the Template Files and Run Transformation on Airflow

1. Create a revised template file based on  ```docker_ecs_ecr_template.py```. You will need to revise the following input arguments for your use. 

``` 
- task_id: a task ID is used in Airflow
- default_docker_args: a dictionary to define input arguments used on ECR, ECS
- dagName: DAG name is used in Airflow. This is what you will see on Airflow UI.
```

More information about the input arguments to 
[register an ECS task using boto3](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/ecs.html#ECS.Client.register_task_definition)
2. Create a ```Dockerfile```.
3. Push the codes for data transformation, Dockerfile, and the revised template file to ```AirflowDags``` repo. 
4. Verify all of your newly pushed codes exist on EC2 under the folder ``` ~/airflow/dags/AirflowDags ```. This can be achieved via SSH connection to the EC2 instance.
5. Launch [Airflow UI](https://fst-apc-airflow.agro.services/admin/).
6. Find your DAG. Turn ON the DAG, and Trigger the DAG.
1. Verify the result from Airflow UI, as well as from ECR, ECS through AWS console.
