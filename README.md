# Automatically Deleting Unused Snapshots to Save AWS Costs

## Problem :
Developers sometimes create EC2 instances with attached volumes and take snapshots for backup. When these instances are terminated, they often forget to delete the snapshots, leading to unnecessary storage costs.

## Solution :
We use AWS to reduce storage costs with a Smart Lambda function. This function checks all snapshots and EC2 instances, and if it finds any snapshots not connected to active EC2 instances, it deletes them. This helps us save money by eliminating unused snapshots.

## Steps :

1. Log into your AWS Console.<br>
2. Navigate to the EC2 Console.<br>
3. In the Instances section, select 'Instances,' and then click on 'Launch Instance'.<br>

![d4](https://github.com/SubodhBagde/AWS-Cost-Optimization/assets/136182792/0dbe6736-143a-4255-9852-42929167f8aa)<br>

4. Next, navigate to the 'Elastic Block Store' section and select 'Volumes'.<br>
5. You will notice that a default volume has already been created for us.<br>
6. Next, click on 'Snapshots,' and then click the 'Create Snapshot' button.<br>
7. In Volume ID section choose your default Volume ID created when we create instance.<br>
8. Next, click 'Next,' provide a name for your Snapshot, and then scroll down and click 'Create Snapshot'.<br>

![d6](https://github.com/SubodhBagde/AWS-Cost-Optimization/assets/136182792/11027127-9c2e-49a6-ba3e-2defd20cd1dd)

9.  After creating a Snapshot, navigate to the Lambda Console and create the function.<br>
10. Next, clear the existing code and replace it with the 'identify_stale_snapshots.py' code.<br>

![d1](https://github.com/SubodhBagde/AWS-Cost-Optimization/assets/136182792/7dae35d7-d97e-4c66-8da1-c2988fe52c1f)

11. Click 'Deploy' to save your changes, and then click 'Test.' It will prompt a page that looks like the one given below.<br>

![d2](https://github.com/SubodhBagde/AWS-Cost-Optimization/assets/136182792/180a1691-a52c-4871-be2c-c6510c9f4a4c)

12. Next, click on 'Create Event'. Once you've created the event, proceed to the IAM Console(Identity and Access Management) and then navigate policies section to create a new policy.
13. In the 'Actions' section, grant permissions for the following actions: DescribeInstances, DescribeVolumes, DescribeSnapshots, DeleteSnapshots.
14. Then scroll down and click 'Add Permissions'.

![d3](https://github.com/SubodhBagde/AWS-Cost-Optimization/assets/136182792/32f5a2be-c18e-4435-b85d-50e2d5e6902f)

15. You can terminate the EC2 instance to test our Lambda function. Under the Code section, click 'Test code', it will display an output like this.

![d7](https://github.com/SubodhBagde/AWS-Cost-Optimization/assets/136182792/b0351f95-91e6-4395-9620-5e8551eb90da)

