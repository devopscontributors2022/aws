# aws


**List of services:**

1.	IAM
2.	S3
3.	EC2 – AMI,ELB,EBS,ASG 
4.	Lambda
5.	SNS
6.	Cloud Front
7.	VPC
8.	AWS CLI
9.	Elastic beanstalk
10.	Code commit, code pipeline
11.	cloud trail
12.	RDS –MySql,  DynamoDb
13.	Cloudwatch
14.	Cloud Formation
15.	API gateway

**IAM: Identity Access Management ** {Youtube video created :Create a video on how to create a aws user from root account and add to Group with policy attached to it !- https://youtu.be/hCaWweuZlSQ}

1.	User ;
2.	Group : Create a group -> Add Users-> Add Policy 
3.	Policy:
a.	JSON format .
b.	Example: AmazonEC2FllAccess
c.	2 types : AWS Managed (600+) and Customer managed policy


4.	Role :
a.	For communication between AWS services 


**EC2 :  AMI,ELB,EBS,ASG**


Create EC2 instance : https://youtu.be/T1Lm484Zgfc - youtube video created for creating linux machine and connecting in to it ! 
    https://youtu.be/DNHtPqI4lpM - connect without ssh or putty video created !!
Launch Types : 
1.	On demand instance : For shorter workload , predictable price
2.	Reserved instance :  F or long workloads (Reserve for > 1 year )
3.	Convertible reserved Instance :  Reserved instance , but RAM from 16 GB -> 64 GB can be changed during performance testing , and brought back once testing done
4.	Scheduled Reserved Instance : i.e., Using only on weekends
5.	Spot Instance : Very cheap
6.	Dedicated Instance : Other customer will not share your hardware
7.	Dedicated Hosts : Book an entire physical server 

User Data in EC2 ?
•	To save time of installing some software give cmd in user data , whenever launching the Ec2 instance automatically all the cmds mentioned will be installed in machine 
How to connect to Linux Ec2 Instance ?
•	In git bash terminal :   Ssh –i <pemfilename.pem>  Ubuntu@<Public IPV4 address>

How to create a snapshot of volume in EC2 ?
Create a snapshot ?

How to create AMI (Amazon machine image)? 
Elastic Load Balancing  (ELB)
•	Round robin method used to distribute the load 
•	Vertical scaling vs Horizontal scaling ? 
VERTICAL SCALING	HORIZONTAL SCALING
1 GB RAM -> 32 GB RAM	1 (1GB RAM)-> 2…N (1 GB RAM)  
Stop the instance , and then modify instance type (t2.nano -> t2.micro or any choice) and start again	Can be achieved using ELB ( Elastic Load Balancer)

ELB Diagram :
Amazon.in -> ELB URL (DNS Name) -> EC2 instance can be increased or decreased based on the load (User can set min instance and max instance to manage the cost and high availability)

3 types of ELB :
	ALB - Application Load Balancer : balance the load based on traffic from HTTP or HTTPS listeners 
	NLB – Network Load Balancer
	GLB - Gateway Load Balance


Creation of ALB : 
•	Name of ALB 
•	Schema : Internet facing
•	IP address type : IPV4
•	VPC :
•	Mappings : Atleast 2 AZs
•	Security groups
•	Listeners and ports {Very important} + Add Target group {Create target group if not available}
o	Listeners : 
	Listeners in ELB ? 
	Its process ; checks /listens to connection request using protocol and port 
	For example : selenium server is running on http and port 4444
	Then , listener protocol and port : http and 4444
	2 types of protocol in general : 
•	Http : 80 
•	Https :443
•	Click on ‘Create load balancer’
•	How to check the ALB working fine ? 
o	Copy and paste DNS name in browser  
Target groups : 
•	Name of target group
•	Target type : Instance 
o	Select respective EC2 instances
•	Select Protocol and Port {For Http://34.4.53.4:4444 then Protocol : HTTP | port : 4444}
•	Health checks
•	Click ‘Target group’
Health Checks ? {Can be configured as part of creating Target Groups}
•	This check is part of ELB creation 
•	To check whether target instance added is working fine 
•	How this achieved ?
o	Path of application url : eg : amazon.in/books ; Then path as /book  | if need to check health of appln root itself e.g amazon.in ; then path as ‘/’
o	Advanced settings : 
	Protocol : HTTP
	Health check path : 
	Interval : 30 -> checks appln health every 30 sec
	Timeout : 5 seconds ->  check for 5 seconds , if no response return as ‘unhealthy’
	Unhealthy threshold : 2 -> If continuously 2 times returns unhealthy , mark the instance as unhealthy 
	Healthy threshold : 5 -> No of times to success should come , to consider a unhealthy target as healthy target again 
	Success codes : 200 -> Http code to consider as success

ASG : Auto Scaling Group 

AMI ?



S3 :  https://youtu.be/L5c10vRhOl8 - Youtube video created for how to create bucket and add file, delete file and bucket !! 
•	Bucket name should be unique across all regions
•	Rules in bucket name : no space and uppercase  
•	In S3 everything is treated as objects
o	Upload -> PUT object
o	Fetch -> GET object
•	Storage limit : NO limit
•	5 GB of data can be stored in a single time ; more than 5 GB can be spitted and stored 
•	If bucket is not exposed to public, while reading the file user will get ACCESS DENIED
•	ACL (Access control list)
o	Object level  - List | write
o	Bucket level – Read | Write 
o	Access can be controlled i.,e everyone | AWS user etc 
•	Encryption:
o	2 types of encryption : 
	Amazon s3 key (Server side encryption-S3)
	AWS Key Mangement service key (SSE-KMS)
•	Static web hosting: 
o	Download the site from https://preview.uideck.com/items/play-bootstrap/  , and the unzip
o	Upload the contents in S3 bucket , and make ACL public 
o	Hit the index.html file url of S3 in browser , to see the result
•	To archive the older data use different S3 storage service :
o	

CLOUD FRONT:

•	Its CDN {Content Delivery Network}
•	Its cache service  - It makes a copy of data
•	Static content will be cached first time , from next time static content will be loaded quickly
•	Example : in Amazon prime , accessing a ‘Master’ movie from Tamilnadu region first time alone request goes to S3 location , from next time if any other user access the same movie , CLOUD FRONT will stream the video quickly instead of going to S3 location 
o	Advantage : Data transfer cost will be reduced 
	Uses the AWS edge locations like Chennai , Bangalore for Mumbai region 
•	Invalidation? 
o	If any file in S3 changes, change will not get directly updated in cloud front , invalidation is required for a particular file level or for bucket level to sync the changes . 
 

RDS : RELATIONAL DATABASE SERVICE  - Structured DBs {NO SQL DB – Dynamo DB}

Why cloud DB ? 

•	Reduce server cost 
•	Reduce DB and server maintenance cost 
Types of RDS ?
•	Amazon Aurora -> Amazon’s DB , built on top of MySQl and PostgreSQL : So migrating MySQL or PostgreSQL to Aurora is pretty easy . 
•	MySQl – Open source 
•	MariaDB– Open source
•	PostgreSQL– Open source
•	Oracle- Paid license –but no need to pay separately for license ; Amazon charges combined single charge for usage + license 
•	Miscorsoft SQL server - Paid license –but no need to pay separately for license ; Amazon charges combined single charge for usage + license 

Advantages of RDS : 
•	Netflix and Hotstar uses AWS 

How to create MySQL RDS ?
•	Choose ‘standard ‘ type -> so that many options can be configured by user 
•	Select RDS – MYSQL 
•	MYSQL Version : 5.6
•	Type : Free Tier | Production | Dev or test  {Free tier : db.t2.micro}
•	DB name : myDemodb
•	Username: admin 
•	Password : AUtogenerate | enter password –admin1234
•	Storage : 
o	Type : SSD -> faster then harddisk 
o	Allocated storage: 20 GB 
o	Storage AUtoscaling  :
	If Enable auto scaling : 21 to 16384 GB 
o	Availability & Durability :
	Multi-AZ deployment : If any AZ is down , another AZ will server 
•	Same copy of data will be available in multi AZ 
o	VPC 
o	Database port : 3306 {default}
o	Database authentication :
	Passwor dauthentication 
o	Database options:
	Database name : 
	Enable automated backups 
•	How many retention backup ? 2 days {user choice}
	Monitoring : 
•	Monitor done by cloud watch {Chargeable ! }
	Maintenance : 
•	Enable auto minor version upgrade – AWS will upgrade automatically based on selected time period 
o	Cost :
	750 hrs of 1 instance free / month for t2.micro 
	 
o	How to access DB ?
	MySQK workbench | HeidiSQL 
	Easy one : Heidisql 
•	Install and open app 
•	What is required to connect ? 
o	Hostname /IP : <End point from db created in AWS >
o	User : 
o	Password : 
o	Port 
o	Possible to take snapshot ? Yes , and able to export to S3 bucket  
    
ELASTIC BEAN STALK
•	Its platform  as service 
•	 It’s free , no need to pay
•	Used to host web apps
•	How to create Elastic Bean stalk ?
o	Application Name : myFirstApp
o	Platform : TOMCAT {select prog lang used to create an application }
o	Platform version : 3.4 
o	Application code : Sample application {AWS will use some sample code}| Upload your code {Upload the application as zip file}
o	Click ‘create environment ‘ -> AWS will take up to 8 mins to create the environment ?? 
	Why 8 mins ? 
•	It will store appln zip file in S3
•	Create respective EC2 machine {No PEM file will be created for EC2 instance here -> as Beanstalk will manage the EC2 instance },security group, target groups, create ELB, create autoscaling 
	How to see appln hosted using beanstalk is running fine?
•	Click on URL generated in beanstalk environment 	
	Possible to redeploy the application ? yes possbible
	Possible to update the default configuration created by beanstalk like EC2 t2.micro -> t3.micro  and other details ? YES possible 
 

CODE COMMIT  {Its developer tool in AWS}
•	Note : 
o	git -> version control system ; 
o	github/gitlab/bitbucket -> Source code management tool {Can be public / private}

Code commit in AWS ?
	Private repository only within AWS , llr to github 
	Pricing ? 
•	Free : up to 5 users , 50 GB , only private repo ; if exceeds costing will apply 
	Built on top of git . 
o	Create code commit repository ?
	Login as IAM user , don’t use root user 
	Create repository > Repository Name ‘myFirstCodeCommitRepo’ > ‘Create’
	Create ‘Git Credentials’ > Goto IAM > Security credentials > Generate credentials for ‘HTTPS git credentials for AWS code commit’’ > Download credentials
	Clone the repository > Copy the repo url ; Create new folder in system -> use Git bash to clone the repository -> o/p: note .git folder will be created 
	Add a sample .txt file in to the repo folder , and commit the code as usual procedure
•	Git add .
•	Git commit –m “Adding text file”
•	Git push 
	Add the sample ‘web app ’code by following same git procedure to commit and push the code 

 
CODE PIPELINE


CLOUD WATCH
•	Its Monitoring service to monitor a  server and other aws services 
•	Various functionalities in cloud watch :
o	Alarms
o	Logs
o	Metrics : Generate and visualize graph to user .Example : Monitor and display the EC2 instance CPU utilization % to user . 
	Youtube video created for this : https://youtu.be/wJT7jaKMp1I
	
o	Events
	Now referred as Amazon Event Bridge  : Created a example below 
    
•	Cloudwatch events example :  https://youtu.be/wJT7jaKMp1I - YOutube video created for cloudwatch scenario !! 
    
	Note : CRON expression scheduled events use UTC time zone (IST is +5:30 hrs ahead of UTC)
Syntax 
cron(fields)
Field	Values	Wildcards
Minutes	0-59	, - * /
Hours	0-23	, - * /
Day-of-month	1-31	, - * ? / L W
Month	1-12 or JAN-DEC	, - * /
Day-of-week	1-7 or SUN-SAT	, - * ? L #
Year	1970-2199	, - * /
o	Stop the instance by 11 PM IST every day ->  0 23  * * ? * (IST) => cron(42 6 * * ? *) 
o	Scenario: Create a cloud watch event using CRON expression  to stop the Jenkins machine automatically every day between 11 PM ? {Yet to create youtube video for this example}
	Cluoud watch events > Amazon Event Bridge (Redirects)> Create a new rule > 
•	Rule name : stop-jenkins-ec2instance
•	Event schedule : CRON Expression 
•	Target : EC2instance | Type : EC2 StopInstances API call | Instance Id <id of instance>
	Output : By everyday 11 PM IST , EC2 instance (Based on instance Id mentioned ) will be stopped 
•	Further customization : Create one more event to take snapshot of the stopped instance 

•	CLOUDWATCH ALARM EXAMPLE USING SNS SERVICE :
o	Scenario : Whenever a CPU utilization of a EC2 machine exceeds the 30 % trigger a alarm using Metrics of cloud watch , then subscribe the SNS topic {Internally SNS topic will have Topics and Subscriptions created } – [create a youtube video for cloudwatch alarm with SNS service ]
 

•	How to increase the load of the CPU to test CPU utilization ?
o	sudo apt install stress-ng
o	sudo stress-ng --cpu 400 -v --timeout 120s
o	top -> to check the cpu utilization % 
•	CLoudwatch pricing part :
o	Free : 
	10 metrics + 10 alarms 
	1 Lakh API requests
    
CLOUD TRAIL
•	For security purpose
•	Continuously log AWS account activity
•	Under Event history > AWS captures and displays all activities performed on a account in last 90 days
•	Customize /filter time period to see logs 
•	Info of region, AWS resource name, system IP used ,AWS access key 
•	

VPC
 
Note : If you use default VPC , private address will always start with 172.31.*.* 
Why VPC creation is required?
•	Same IP range can be provided to different companies if they create their own VPC , instead of using default VPC . 
•	Increases security ,since each company will not know other company IP address range . 
 

Architecture of VPC ?
•	Internet Gateway : Similar to LAN ; connects the VPC with internet 
•	Routing table : similar to Router ; routes the requests to respective subnets (AZ’s) based on IP range 
•	Subnets : its AZ’s 
o	
 


How IP address are managed / allocated?
•	Using CIDR (Classless Inter-Domain Routing)
•	 
•	
•	IP address allocation can be understood in cidr.xyz site 

o	0.0.0.0/0 -> If routing prefix  is 0, all 4 blocks in IP address can be changed 
o	10.0.0.0/8->  If routing prefix  is 8, Last 3 numbers can be customized   
o	10.0.0.0/16 ->  If routing prefix  is 16, Last 2 numbers can be customized   
o	10.0.0.0/24-> If routing prefix  is 24, , Last 1 number can be customized   10.0.0.0/32-> If routing prefix  is 32 , All fixed no customization
•	Some IP address starting numbers will be reserved namely :
o	0- 126 -> realtime {For eample 0.0.0.0/0 -> 126.0.0.0/0}
o	127 -> reserved
o	128 – 223 -> Realtime
o	224-239 - Military
o	240-255 – Research 


Creating a VPC (Virtual Private Cloud) :
 
Note : In security group , 
•	Inbound rule : Rule to connect from Internet -> EC2
•	Outbound rule : Rule to connect from EC2 -> Internet

AWS CLI {Create youtube video for what is CLI in AWS and how to connect your windows machine with AWS via CLI? }
•	Create IAM Access key and Id {its mandatory to perform AWS CLI } for a aws user not for root user
•	Install aws cli in windows machine
o	How to install CLI ?
	https://awscli.amazonaws.com/AWSCLIV2.msi -> Download and install in machine 
	In cmd : aws –version ; will show version of aws installed 
•	Connect AWS with windows machine via AWS CLI using user key id and secret key as below 
 

•	Test the CLI ?
o	Scenario {youtube video need to prepare}
	Create a S3 bucket , add a file (copy file) from your system to S3 , and check is file uploaded in S3 . 
•	Aws s3 mb s3://create-bucket-krish-demo-12022022  //mb -> make bucket
•	Aws s3 ls
•	Aws cp <full path of file> s3://create-bucket-krish-demo-12022022  
•	Aws s3 ls // crated file should get displayed ! 

 
	Delete the created bucket and its respective files (i.e., objects)
•	Aws s3 rb s3://create-bucket-krish-demo-12022022 – -force // force is to delete bucket with files in to it !
 
	Delete created file or object from respective S3 bucket
•	Aws s3 rm s3:// create-bucket-krish-demo-12022022/ Kavin_StoryOfColorChicken.mp4
 
	Move files from one s3 bucket to another s3 bucket 
•	Cmd : mv 
•	Aws s3 mv < from bucket path > < to bucket path >




CLOUD FORMATION


LAMBDA
•	LIST OF POSSIBLE AWS LAMBDA AUTOMATION SCENARIOS AND SOLUTIONS
SNS , SES
API GATEWAY
ROUTE 53 



PUTTY :
•	SSH protocol used to connect with linux machines 
Different ways to connect with EC2 instance ?
•	Linux : 
o	Via Command prompt : ssh –i <pemfile.pem> Ubuntu@<public IPV4 address> | ssh –i <pemfile.pem> ec2-user@<public IPV4 address>

o	Via gitbash :  use same command as like command prompt connection 
•	Windows :
o	RDC (Remote Desktop Connection)
