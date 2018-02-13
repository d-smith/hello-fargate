# hello fargate

This project contains some cloud formation to spin up a fargate
service that runs nginx in a container, fronted by a load
balancer. This shows how Fargate ties into existings constructs
such as VPCs and load balancers.

Some links

* [Fargate vis the CLI](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ECS_AWSCLI_Fargate.html)
* [Task Definitions for Fargate](https://aws.amazon.com/blogs/compute/migrating-your-amazon-ecs-containers-to-aws-fargate/)
* [AWSVPC Networking for Containers](https://aws.amazon.com/about-aws/whats-new/2017/11/amazon-ecs-introduces-awsvpc-networking-mode-for-containers-to-support-full-networking-capabilities/)
* [Load Balancers via the CLI](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/tutorial-application-load-balancer-cli.html)
