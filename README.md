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

----------------------------------------------------


### Project: 
  * Automate configuring EC2 Server Instances
### Technologiesused:
  * Python, Boto3, AWS

### Project Description:
* Write a Python script that automates adding environment tags to all EC2 Server instances


  ** Create 2 ec2 instance in paris region and 1 ec2 instance in frankfurt region
1. Boto3 Setup:
* Creates EC2 clients and resources for the Paris (```eu-west-3```) and Frankfurt (```eu-central-1```) regions.

2. Retrieve Instance IDs for Paris Region:
* Calls ```describe_instances()``` on the EC2 client for Paris to get instance data.
* Iterates over the reservations and instances to collect instance IDs in the ```instance_ids_paris``` list.

3. Apply "prod" Tag in Paris:
* Used ```create_tags()``` to apply a tag with the key ```'environment'``` and the value ```'prod'``` to all instances in the Paris region.

4.Retrieve Instance IDs for Frankfurt Region:
* Similarly, calls ```describe_instances()``` for the Frankfurt region to retrieve instance IDs in the ```instance_ids_frankfurt``` list.
5. Apply "dev" Tag in Frankfurt:
* Used ```create_tags()``` to apply a tag with the key ```'environment'``` and the value ```'dev'``` to all instances in the Frankfurt region.

 * it helps categorize EC2 instances by environment ("prod" for Paris and "dev" for Frankfurt) for organization.

### Frankfurt Region:

![describe_instance_status - Boto3 1 28 51 documentation - Google Chrome 21-09-2023 10_20_20](https://github.com/Rajib-Mardi/Automation-with-Python1/assets/96679708/c6452197-b805-4440-8b85-df3b0a09ef8a) 


### Paris Region: 
![describe_instance_status - Boto3 1 28 51 documentation - Google Chrome 21-09-2023 10_20_36](https://github.com/Rajib-Mardi/Automation-with-Python1/assets/96679708/1d4bf127-f3d0-41e7-87c0-798513f58ea1)

-------------------------------------


