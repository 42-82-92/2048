# Scenario

Your boss asks you to build a POC. The product manager has a new game hitting the market (2048) and he wants you to take the code from the dev team, containerize the app, and provide a highly available (hint: Multi-AZ) environment to run the game in containers. It should scale automatically, update quickly when the code is updated, and remove the need for administrators to manage Kubernetes.

## Tasks

Do some research on ECS to understand the components (what is a Service? what is a Task? what is a Task Definition? etc...)

Next, build an ECS cluster with your 2048 container image and use an ALB as your endpoint. Hit that in a browser and confirm it works

## Knowledge

### Service

This is like an orchestrator. It manages all tasks, load balancing, and that you always have N number of tasks running at all times. So if an instance has a fatal error, the service is what would manage replacing that instance with a fresh one.

### Task

Tasks cannot be configured to use a load balancer, only Services can.

### Task definition

Task definitions are collections of container configurations (which image to use, ports to expose, CPU and memory allotments.)

### How do they interact with each other?

Services run your tasks, which use Task Definitions to run instances.

A container instance can run many tasks, from the same or different services.

Tasks cannot be configured to use a load balancer, only Services can.

### ECS Container Agents

The work of ECS is done on EC2 instances with docker and the ECS Container Agent installed. The agent takes care of the communication between ECS and the instance, providing the status of running containers and managing running new ones.  

## Summery

We have seen how a Dockerized application can be represented by a **Task Definition** that has a one-to-one relationship with a **Service** which in turn uses it to create many different **Task** instances.

This **Service** is deployed to a **Cluster of ECS Container Instances** that provide the pool of resources needed to run and scale your application. Additional Services can be deployed in to the same Cluster.

Amazon ECS, or any container management service, aims to make this as simple as possible, abstracting away many complexities of running infrastructure at scale.

Check out Code Camp's deep dive into ECS:
<https://www.freecodecamp.org/news/amazon-ecs-terms-and-architecture-807d8c4960fd/>
