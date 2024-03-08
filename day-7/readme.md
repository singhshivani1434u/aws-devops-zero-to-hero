Steps:
01. create vpc > vpc and more, aws-prod-project, nat gateway 1 per az, none > create
02. ec2 > auto scaling groups > aws-prod-autoscaling-group [ create a launch template > aws-prod-template , description , ami ubuntu , t2 micro ,
keypair , create security group > aws-prod-sg , all ssh access , select vpc id that u created , inbound rules port 8000 , 22 >launch template] 
Select the launch template u created. 
03. Next > select vpc > select PRIVATE availability zone and subnets 
04. Next > No load balancer > defaults
05. Next > Desired capacity 2, Minimum 1, Maximum 4 > None 
06. Next > Next > Next > Create auto scaling group
07. Check instance created in diff az. it will hot have public ip. 
[To login into this two instances, create a bastion host i.e another ec2 instance]
08. Launch ec2 instance > bastian host, ubuntu, t2 micro , vpv id u created, public subnet , enable public ip , create sg > launch > connect via ssh > copy pem file from local computer to bastian host.
Command : scp -p [path of pem file] pemfilename ubuntu@public ip of bastian:/home/ubuntu
09. to login into the other ec2 instances from bastian host
Command : ssh -i pemfile ubuntu@private ip
10. after login > create index.html and paste any html code > save > python3 -m http.server 8000 . Repeat it for another ec2 instance and edit the code or paste different code
11. Create application load balancer > aws-prod-lb > default >vpc id u created > pickup both az > Public subnet > aws-prod-sg {edit inbound aloow http port 80} >
[Create target group > instances > aws-prod-target-group > default , port 8000 , vpc id u created > select instances > port 8000 > include as pending >create target group]
listener port 80  > create load balancer
12. copy dns name of load balancer and access it on internet
