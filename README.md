# AirflowDAGs
This repository automatically syncs with the Airflow instance running on AWS every minute on the master branch. <br> 
The repo provides template to build your own data transformation process in a scalable and flexible way on AWS using Airflow. <br>

##  Using Airflow to Orchestrate Data Transformation on AWS

Airflow uses directed acyclic graphs (DAGs) to manage and monitor workflow orchestration. <br>
The following diagram illustrates the architecture of using Airflow to orchestrate data transformation on AWS. <br>

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
1. Choose ``` airflowhelloworld ```
1. Turn ```On``` button for ``` airflowhelloworld ```. Then click ```Trigger DAG```.
1. Choose ```Graph View``` to monitor the 3 subprocesses in a DAG.
1. From AWS console, you can verify whether a Docker image is pushed to ECR, and whether an ECS task is created and run.

* Go to ECR: check if the Repository ``` airflowhelloworld ``` exists.
* Click ``` airflowhelloworld ``` repository, verify if a Docker image exists.
* Go to ECS: under Task Definitions, choose ```airflowhelloworld``` and verify if a new task is created.
* Go to ECS: choose ```Clusters```. Choose ```fargate``` cluster.
* Click ```Tasks``` tab, select a Task with its Task Definition starting with ```airflowhelloworld```. You can select that task and monitor its status.

## How to Use the Template Files and Run Transformation on Airflow

1. Create a folder, which will include Dockerfile, template file, and your data transformation codes later.
2. Revised template file based on  ```docker_ecs_ecr_template.py```. You will need to revise the following input arguments for your use. 

``` 
- DIR_NAME: directory name of all the files. It will be used as the task name and DAG name in Airflow, repository name in ECR, and task name in ECS as well.
```

More information about the input arguments to 
[register an ECS task using boto3](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/ecs.html#ECS.Client.register_task_definition)

3. Create a ```Dockerfile```.
4. Push the codes for data transformation, Dockerfile, and the revised template file to ```AirflowDags``` repo. 
5. Verify all of your newly pushed codes exist on EC2 under the folder ``` ~/airflow/dags/AirflowDags ```. This can be achieved via SSH connection to the EC2 instance.
6. Launch [Airflow UI](https://fst-apc-airflow.agro.services/admin/).
7. Find your DAG. Turn ON the DAG, and Trigger the DAG.
8. Verify the result from Airflow UI.
9. Verify the result from ECR, ECS, the logs from CloudWatch through AWS console..
