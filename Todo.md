# Scenario:

Your boss asks you to build a POC. The product manager has a new game hitting the market (2048) and he wants you to take the code from the dev team, containerize the app, and provide a highly available (hint: Multi-AZ) environment to run the game in containers. It should scale automatically, update quickly when the code is updated, and remove the need for administrators to manage Kubernetes.

## Tasks:

Do some research on ECS to understand the components (what is a Service? what is a Task? what is a Task Definition? etc...)

Next, build an ECS cluster with your 2048 container image and use an ALB as your endpoint. Hit that in a browser and confirm it works

## Knowledge

### Service  

This is like an orchestrator. It manages all tasks, load balancing, rules and makes sure you always have N number of tasks running at all times. So if an instance has a fatal error, the service is what would manage replacing that instance with a fresh one. or if CPU usage is to high, your task could add another instance to share the load. 

### Task

Tasks are simply instances of task definitions, running the containers detailed in the task definition. Multiple tasks can be created by one task definition (like for scaling).
Tasks cannot be configured to use a load balancer, only Services can.

### Task definition

Task definitions are collections of container configurations (which image to use, ports to expose, CPU and memory allotments). These act like the blueprints of the hole operation.


How do they interact with each other?

Tasks cannot be configured to use a load balancer, only Services can.

Check out Code Camp's deep dive into ECS:
https://www.freecodecamp.org/news/amazon-ecs-terms-and-architecture-807d8c4960fd/
