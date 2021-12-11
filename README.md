
# Exercise and Purpose
This challenge is meant to provide an opportunity for DevOps candidates to demonstrate understanding of the problem domain, ability to implement, and provides flexibility to really "show off" any particular skillsets a they would like.

The end result should be a Github Repository on your Github account, configured to public or private with read access for the users [walked](https://github.com/walked) and [donthorp](https://github.com/donthorp) 

This repository should include:
- A brief summary of your implementation.
- Instructions for implementation (deployment of the environment, accessing, etc)
- Any notes, wrinkles, or unexpected behaviors you encountered
- Future improvements you may make
- And your solution (infrastructure code, any CI/CD, dockerfile, etc)

## A few notes:
First: If you have any questions at all - please ask! 

This exercise is built to leverage AWS for use. If you have a strong preference you may use an alternative cloud provider. For AWS, we recommend the [AWS Free Tier](https://aws.amazon.com/free/?all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc&awsf.Free%20Tier%20Types=*all&awsf.Free%20Tier%20Categories=*all)

Additionally, this is not a "pass/fail" exercise. We are aiming to evaluate problem solving tactics, thought process, and general intuition. 
- If you get stuck: That's ok - document where, what you tried, and what could be happening.
- If you have no difficulty at all: Cool! show us where this could be improved. Check out the `Bonus Points` section. Show us what _you_ are thinking about while creating this solution.

# The Challenge:
Cloud technology often uses a common core set of technologies; for this exercise we're going to focus on a few particular items:
1) Infrastructure-as-Code
2) Docker
3) Microservices and/or distributed stateless applications

As such, we'd like to ask you to, using any Infrastructure-as-Code tool you would like (Terraform, CloudFormation, Pulumi, etc):

### Application:
Create a Dockerfile that will build a container which runs [Caddy](https://github.com/caddyserver/caddy) webserver. This should be configured to run in `file-server` mode with the `--browse` flag

Core container requirements:
- The root path for Caddy is configured so it can be overridden via environment Variable
- Container is exposed on port 3001 and is generally network accessible
- The root path of the Caddy server should have the contents of the `/srv` folder 
- Is pushed to a publicly accessible Registry (e.g. Docker Hub) or a private registry that can be accessed by your infrastructure code (e.g. ECR)

### Infrastructure:
Write a basic IAC configuration to deploy and bootstrap an EC2 (or comparable) instance, this should include pulling the aforementioned docker image, and running it on the EC2 instance indefinitely. 

Infrastructure Requirements:
- Deploys an EC2 with a Public IP address into a VPC (default VPC is acceptable for this)
- At instantiation will install Docker, pull the Docker image, and begin listening for HTTP requests

## Bonus Points:
If you have additional time, additional items that can be considered:
- Creating the Infrastructure-as-Code to define an EFS store (or alternative) and mount that to the EC2 instance at runtime (possibly pointing Caddy at that endpoint)
- Configuring Load-Balancing and an Auto-Scaling Group instead of a singular EC2 instance.
- Implementing some form of CI/CD (GitHub Actions likely being simplest) to rebuild the Docker container on a merge to master..
- And subsequently triggering a redeploy of the environment on the new container



