---
aliases: 
date: 2020-07-15
description: 
published: true
keywords: 
layout: note
title: AWS ECS
tags:
  - aws
  - devops
---

## What is ECS?
ECS is Amazon their own take to make a container orchestrator, before surrendering to Kubernetes (therefore, [[AWS EKS]])

## Components
- Task definition: define a job that will be run on the container(s), define also the container(s) resources. One *task definition* can create several *tasks*
- Task: is an instance of a task definition.
- Service: how many tasks you want to run for how long (at least this is my understanding)

### Resources
[What is the difference between a task and a service in AWS ECS?](https://stackoverflow.com/questions/42960678/what-is-the-difference-between-a-task-and-a-service-in-aws-ecs)
[A beginner's guide to Amazon's Elastic Container Service](https://www.freecodecamp.org/news/amazon-ecs-terms-and-architecture-807d8c4960fd/)

## Pricing
Traditional ECS under the hood provisions EC2 instances to build a cluster, where the user pays for the EC2 instances.

*Fargate* is the "Serverless" version of the above where the user pays for the time of running.