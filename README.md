# Automated-EC2-health-checks-configuration-and-backup-restore.

it  uses the boto3 library to interact with AWS EC2 instances and the schedule library to run a task periodically.

EC2 Client Setup: It initializes a boto3 EC2 client for the eu-central-1 region.

check_instances_status Function: It calls the describe_instance_status API to get the status of all EC2 instances, including the instance status and system status. For each instance, it prints:

Instance ID
Instance state (e.g., running, stopped)
Instance status (e.g., ok, impaired)
System status (e.g., ok, impaired)
Scheduling: The function is scheduled to run every 5 seconds using schedule.every(5).seconds.do(check_instances_status).

Main Loop: The script continuously runs, checking the status of EC2 instances every 5 seconds.

it helps in monitoring EC2 instance health and status in real-time.
