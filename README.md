### Written automation scripts for EC2 Health Checks, configuring EC2 instances, Data Backup and Restore
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
  






<img src="https://github.com/user-attachments/assets/fbb61666-9c3b-49cf-ace7-340b001495a1" width="700"> 


----------------------------------------------------


### Project: 
  * Automate configuring EC2 Server Instances
### Technologiesused:
  * Python, Boto3, AWS

### Project Description:
* Write a Python script that automates adding environment tags to all EC2 Server instances

* Create 2 EC2 instances in the Paris region and 1 EC2 instance in the Frankfurt region.

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







<img src="https://github.com/user-attachments/assets/a673dd5d-afa3-46c2-becd-eeb97f4a9932" width="700"> 



### Paris Region: 






<img src="https://github.com/user-attachments/assets/5bc93888-2018-4ca4-b850-8b56be0128bf" width="700"> 



-------------------------------------

###  Project: 
  * Data Backup & Restore
### Technologiesused: 
Project Description:
  * Python, Boto3, AWS

### Project Description:
  ### Write a Python script that automates creating backups for EC2 Volumes


 *  Create a ec2 instance in aws manually  and tag the name of volume as the "prod" and use pyhon script to create a snapshot out of it

* It creates snapshots of volumes that are tagged with the name "prod." It employs the "schedule" library to schedule and run the volume snapshot creation process at regular intervals.

1.EC2 Client Initialization:
* ```boto3.client('ec2')```: Initializes a connection to the AWS EC2 service using the ```boto3``` library.
* ```region_name="eu-west-3"```: Specifies the AWS region (Paris) for the EC2 service
2.  Create Snapshot Function:
* ```describe_volumes()```: Retrieves details about EC2 volumes.
* Filters: Filters the volumes by the ```Name``` tag, only retrieving volumes tagged with ```prod```.
* For each volume in the response (```volumes['Volumes']```), the script creates a snapshot using ```create_snapshot()``` with the volume ID.
* ```print(new_snapshot)```: Prints the snapshot details after creation.

3. Scheduling with ```schedule```:
* The schedule library is used to run the ```create_volume_snapshot()``` function every 30 seconds.

4. Infinite Loop:
* The ```while True``` loop keeps the script running continuously, checking every second if there is any pending task to run (i.e., the scheduled snapshot creation).








<img src="https://github.com/user-attachments/assets/12512a23-7bbe-4314-9c33-751a6de51fd1" width="700"> 


-------

### Write a Python script that cleans up old EC2 Volume snapshots

* if snapshots run everyday , we end up with lots of snapshots
* this script fetches volumes tagged with ```Name=prod```, then retrieves and sorts their snapshots by date.
* It deletes all snapshots for each volume, keeping only the two most recent ones.


1. EC2 Client Initialization:
* Initializes a connection to the EC2 service in the ```eu-west-3``` (Paris) region.

2. Fetching Volumes with ```Name=prod```:
* ```describe_volumes()```: Retrieves all EC2 volumes that are tagged with Name=prod
   
3. For Each Volume, Fetch Snapshots:
* For each volume, the script fetches the snapshots associated with it (```describe_snapshots```), filtered by ```OwnerIds=['self']``` to get only snapshots owned by the user.

4. Sort Snapshots by Date:
* The snapshots are sorted by the ```StartTime``` field in descending order (newest snapshots first) using ```itemgetter('StartTime')```.

5. Delete Older Snapshots (Keep 2 Latest):
* It deletes all snapshots except for the two most recent ones (using ```sorted_by_date[2:]``` to skip the first two).
* The ```delete_snapshot()``` method deletes each older snapshot, and the response is printed.







<img src="https://github.com/user-attachments/assets/675c1a2b-60bf-49a0-b92b-2fc6347f7ee1" width="700"> 


---------

### Write a Python script that restores EC2 Volumes

* This script finds the latest snapshot of a volume attached to a specified EC2 instance, creates a new volume from that snapshot, and then attaches the new volume back to the same instance.

1. EC2 Client and Resource Initialization:
* ```ec2_client```: Used for making low-level EC2 API calls (like describing volumes and snapshots).
* ```ec2_resource```: Provides higher-level abstractions for managing EC2 resources (like volumes and instances).

2. Fetching Volumes Attached to an Instance:
* Retrieves volumes attached to the specified EC2 instance (```instance_id```).

3. Fetching Snapshots for the Volume:
* Fetches all snapshots of the volume attached to the instance by filtering with the volume ID.


4. Sorting Snapshots by Date:
*  Sorts the snapshots by their ```StartTime``` in descending order, keeping the most recent snapshot.

5. Creating a New Volume from the Latest Snapshot:
* Creates a new EBS volume in ```eu-west-3c``` using the latest snapshot, and tags it with ```Name=prod```.

 6. Waiting for the Volume to Become Available:
* The script continuously checks the state of the newly created volume until it is in the ```available``` state.
* Once available, it attaches the new volume to the instance at device ```/dev/xvdab```.









<img src="https://github.com/user-attachments/assets/d833d0e8-44e5-40c0-af0b-2312f7cd2497" width="700"> 







<img src="https://github.com/user-attachments/assets/1342294c-a555-4e7f-86cd-a4c34769a64e" width="700"> 

