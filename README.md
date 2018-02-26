# hello fargate

This project contains some cloud formation to spin up a fargate
service that runs nginx in a container, fronted by a load
balancer. This shows how Fargate ties into existing constructs
such as VPCs and load balancers.

To install:

1. Copy the templates to a deployment bucket

<pre>
aws s3 cp . s3://deploy-bucket --exclude "*" --include "*.yml" --recursive
</pre>

2. Install the stack

<pre>
aws cloudformation create-stack \
--stack-name stackName \
--template-body file://fgstack.yml \
--parameters ParameterKey=BucketRoot,ParameterValue=https://s3.<region>.amazonaws.com/<bucket>
</pre>

After the stack is installed, you can get the DNS name by first figuring out the load balancer stack name, then getting the dns name by looking at the stack outputs.

You can use the CLI to get stack names:

<pre>
aws cloudformation list-stacks --stack-status-filter CREATE_COMPLETE --query 'StackSummaries[*].{name:StackName}' --output text
</pre>

One you know the stack name you can grab the DNS name:

<pre>
aws cloudformation describe-stacks --stack-name c2-LoadBalancer-1QKGZWZAAFYU0 --query 'Stacks[0].Outputs[?OutputKey==`LoadBalancerDNSName`]'
</pre>

Once you have the load balancer DNS name you can curl the endpoint

<pre>
export http_proxy=proxyAddress
curl dnsName
</pre>

Some useful links

* [Fargate vis the CLI](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ECS_AWSCLI_Fargate.html)
* [Task Definitions for Fargate](https://aws.amazon.com/blogs/compute/migrating-your-amazon-ecs-containers-to-aws-fargate/)
* [AWSVPC Networking for Containers](https://aws.amazon.com/about-aws/whats-new/2017/11/amazon-ecs-introduces-awsvpc-networking-mode-for-containers-to-support-full-networking-capabilities/)
* [Load Balancers via the CLI](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/tutorial-application-load-balancer-cli.html)
