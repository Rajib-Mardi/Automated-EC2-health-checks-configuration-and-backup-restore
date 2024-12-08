### Project:
* Health Check: EC2 Status Checks
### Technologiesused:
* Python, Boto3, AWS, Terraform
### Project Description:
 *  Create 3 EC2 Instances with Terraform

* Python script to continuously check the status of EC2 Instances in a specific interval
* it  uses the ```boto3``` library to interact with AWS EC2 instances and the ```schedule``` library to run a task periodically.

1. EC2 Client Setup: It ```initializes``` a boto3 EC2 client for the ```eu-central-1``` region.

2. ```check_instances_status``` Function: It calls the ```describe_instance_status``` API to get the status of all EC2 instances, including the instance status and system status. For each instance, it prints:

* Instance ID
* Instance state (e.g., running, stopped)
* Instance status (e.g., ok, impaired)
* System status (e.g., ok, impaired)
3. Scheduling: The function is scheduled to run every 5 seconds using ```schedule.every(5).seconds.do(check_instances_status)```.

4. Main Loop: The script continuously runs, checking the status of EC2 instances every 5 seconds.

* it helps in monitoring EC2 instance health and status in real-time.
  
![Automation-with-Python – healthCheckEc2 py 21-09-2023 09_34_47](https://github.com/Rajib-Mardi/Automation-with-Python1/assets/96679708/72bf8c90-7496-4621-9649-5cfcbfb0c07c)
