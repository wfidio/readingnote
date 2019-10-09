#### Cloud computing service models

- Infrastructure as a Service(IaaS)
- Platform as a Service(PaaS)
- Software as Service(SaaS)

#### Common Problems encountered at AWS
- Underlying hardware failures.

- Over-provisioning

- Under-provisioning

- Replication

- Redundancy

- Improving the end-user experience

- Monitoring and log-gathering

#### Basic Patterns

- Snapshot Pattern
This pattern is the basis for many other patterns and includes the way to create an S3-backed,point-in-time snapshot of a running instance.

- Stamp Pattern 
This pattern is called stamp pattern because it covers how to replicate a bootable operating system similar to a rubber stamp of sorts. By creating an image of an operating system that is pre-configured for a purpose, it can be easily replicated by simply bringing it up when need in the same way a stamp works by creating a template.

- Scale up Pattern
The scale up pattern is method that allows a server to change size and specifications dynamically, and as needed.
A benefit of this method is that, if the processing peak can be predicted, such as the beginning of the month or the end of the month, this method can be automated.

- Scale out pattern
A more important issue is to add processing power without affecting the client or the systems interacting with our services. To do this, we will tie together a few different EC2 resources.
The general process for this pattern is:
    - Create an elastic load balancer with forwarding ports and health checks.
    - Create an launch configuration for the instance.
    - Create an auto scaling group with configured CloudWatch alarms and scaling policies.


- On-demand disk pattern
The on-demand disk pattern is similar in nature to the scale up pattern, in that it operates on an already running instance and requires some downtime.
The benefit of on-demand disk size is that you do not need to plan ahead for disk resources. Once the instance is running, you can simply resize its volume when it gets to its maximum capacity.


#### Pattern for High Availability 

- Multi-server pattern
Consider a two-tier architecture in which there is a User Interface(UI) instance that connects to a database instance. Suppose that this system gets a large burst of traffic. Using the scale out pattern, the operations team can manually or automatically add more UI instances to the load balancer to mitigate the flux in traffic. This server redundancy pattern is called multi-server pattern. This pattern includes a health check on the instance so that, if one of the instances that the load is being distributed across is misbehaving, it will not continue to route into it.


- Create an EC2 instance that services HTTP content.
- Create an ELB that services traffic to the EC2 instance.
- Clone the EC2 instance using the stamp pattern.
- Add the newly created instance to the ELB