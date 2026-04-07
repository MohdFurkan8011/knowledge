## AutoScalling

- [What is autoscalling](#what-is-autoscalling)
- [How Auto Scaling Works](#how-auto-scaling-works)
- [Types of Auto Scaling](#types-of-auto-scaling)
- [Architecture Example](#architecture-example)
- [Advantages](#advantages)
- [Health Checks in Auto Scaling](#health-checks-in-auto-scaling)
- [Cooldown Period](#cooldown-period)
- [Lifecycle Hooks](#lifecycle-hooks)
- [Instance Termination Policy](#instance-termination-policy)


### What is autoscalling

**Auto Scaling** automatically adds or removes servers (instances) depending on the traffic load.
It helps to:
- Handle high traffic automatically
- Reduce cost when traffic is low
- Maintain high availability

In AWS, it mainly works with Amazon EC2 Auto Scaling.

**Simple Real Life Example**

Imagine you run an e-commerce website.

- Normal traffic → 2 servers are enough
- Festival sale → traffic increases → need 10 servers
- Night time → traffic decreases → need only 2 servers

Instead of manually creating servers, Auto Scaling does this automatically.

**Points**

- Creating of group of EC2 instances that can scale up or down depending on the condition you set
- Enable elasticity by scalling **Horizontal** through adding or terminating EC2 instances.
- Autoscalling ensure that you have the right number of AWS instaces for your need at all time
- Autoscalling helps you save cost by cutting down the number of EC2 instances when no need
- If autoscalling finds that the number of EC2 instaces launched by ASG into subject AZs is not balanced than Autoscalling does that part
- While rebalancing, ASG lauches new EC2 instance where there are less EC2 at present and then terminates the instace from AZs
- **Adding instace into ASG**
  - Instance must be in running state
  - AMI used to launched the EC2 still exists
  - Instance is not the part of another ASG
  - Instance is in the same Region/AZs 
- We can attach one or more than one Elastic Load Balancer to one ASG
- We can also set up email configuration to send email as instance added/terminated/failed to launch/failed to terminate
- we can merge two ASG 
- **Launch configuration can not be edited after once launched**


### How Auto Scaling Works

Auto Scaling uses three main components:
- **1. Auto Scaling Group (ASG)**
    A group of EC2 instances that AWS manages.
    Example configuration:
    - Minimum instances → 2
    - Desired instances → 3
    - Maximum instances → 10
    
    Meaning:
    AWS will always keep at least 2 servers running
    Normally it keeps 3
    It can scale up to 10 if needed

- **2. Scaling Policies**
    Rules that decide when to add or remove instances.
    Example:
    Scale out (add server):
    > If CPU > 70%
    Scale in (remove server):
    > If CPU < 30%

    These metrics usually come from Amazon CloudWatch.

- **3. Launch Template / Launch Configuration**
    This defines how new servers should be created.
    It includes:
     - AMI (OS image)
     - Instance type (t2.micro, t3.medium etc.)
     - Security group
     - Key pair
     - Storage
    When scaling happens, AWS launches new EC2 instances using this template.

### Types of Auto Scaling

- **1. Dynamic Scaling**
    Automatically adds/removes instances based on metrics like:
    - CPU
    - Memory
    - Network traffic

    **Types:**
      - Target - CPU utlization we set 70%, then it keeps traffic near 70%
      - Simple - It will lanuched numbers of instaces as you defined
      - Step scalling - we can add step, like this 50%-60% one instace, 60%-70% launch two instaces

    Example:
    - CPU > 70% → add instance
    - CPU < 30% → remove instance

- **2. Scheduled Scaling**
    Scaling happens at a fixed time.
    Example:
    - 9 AM → scale to 10 instances
    - 11 PM → scale back to 2 instances
    Useful for predictable traffic.

- **3. Predictive Scaling**
    AWS predicts future traffic using ML and scales automatically.

### Architecture Example
```
Users
   ↓
Load Balancer
   ↓
Auto Scaling Group
   ↓
Multiple EC2 Instances
```

### Advantages

- High availability
- Cost optimization
- Automatic scaling
- Fault tolerance

### Health Checks in Auto Scaling

Auto Scaling continuously checks instance health using:
- **1. EC2 Health Check**
    EC2 Health Check
    - Instance stopped
    - Hardware failure
    - Network failure

- **2. ELB Health Check**
    If you use Elastic Load Balancing, it performs additional health checks.
    > /health endpoint
    ```
    Terminate instance
    Launch new instance
    ```

### Cooldown Period

After scaling occurs, Auto Scaling waits before next action.
> Cooldown = 300 seconds
Because new instances need time to:
- boot
- start application
- receive traffic

Without cooldown → **continuous scaling loops.**

### Lifecycle Hooks

Lifecycle hooks allow custom actions during scaling events.
Example:
Before instance termination:
```
Run script
Backup logs
Send metrics
```

### Instance Termination Policy

When scaling in, Auto Scaling must decide which instance to terminate.

Policies include:
- Oldest Instance
- Newest Instance
- Closest to next billing hour
- Oldest Launch Template