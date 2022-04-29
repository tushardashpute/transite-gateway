# transit-gateway

Without Transit Gateway

![image](https://user-images.githubusercontent.com/74225291/165943139-c2c443d0-a4df-43e4-a6c4-86108c52d168.png)


With Transit Gateway

![image](https://user-images.githubusercontent.com/74225291/165943351-f6f7aca7-e879-4d66-b7f0-17c3cc7c6950.png)

Routing Sample:

![image](https://user-images.githubusercontent.com/74225291/165943418-c30948dc-a198-4cbb-82b0-9ed13c5be8c9.png)


Here we are doing the setup of Transite gateway on same aws account across three diffrent VPC's.

Demo Setup:
		
<img width="396" alt="image" src="https://user-images.githubusercontent.com/74225291/165944695-5c42ceba-0c20-4802-9e7f-f8488e0e9ee3.png">

**Steps:**

1. Create 3 VPC's and public and private subnets using below cloud formation tempalates.

	aws cloudformation --region us-east-2 create-stack --stack-name vpc1 --template-body file://vpc1_cfn.yaml
	aws cloudformation --region us-east-2 create-stack --stack-name vpc2 --template-body file://vpc2_cfn.yaml
	aws cloudformation --region us-east-2 create-stack --stack-name vpc3 --template-body file://vpc3_cfn.yaml

2. Now create EC2 instance in each VPC's private subnet.
	
<img width="1223" alt="image" src="https://user-images.githubusercontent.com/74225291/165961540-818c5095-c3f2-4927-a556-fb79c6dd40a7.png">

3. Now will create transit gateway in default VPC
	
Uder VPC --> Transit Gateways --> create transit gateway
	
<img width="1482" alt="image" src="https://user-images.githubusercontent.com/74225291/165961844-98e53167-ae79-4a89-83ee-53aef6fdd3ce.png">

<img width="1444" alt="image" src="https://user-images.githubusercontent.com/74225291/165962094-65d37752-f0f6-4c11-98d8-0ba3194403f3.png">

Keep all default options as it is.

<img width="1510" alt="image" src="https://user-images.githubusercontent.com/74225291/165962281-eb07179a-6c2f-4ede-8eac-40c793ca4a3d.png">

<img width="1255" alt="image" src="https://user-images.githubusercontent.com/74225291/165962647-a3d68cff-38eb-4c7f-a9c5-298e2ebfd9c0.png">


4. Create transit gateway attachment to all 3 vpc's

Goto VPC --> TRANSIT GATEWAYS --> Transit gateway attachments --> Create transit gateway attachment

<img width="1472" alt="image" src="https://user-images.githubusercontent.com/74225291/165965622-1389de84-0ee6-4d74-9444-aba51f63661d.png">

Select private subnet.

<img width="1475" alt="image" src="https://user-images.githubusercontent.com/74225291/165965950-aae0d1cf-c9c1-46e7-b9c4-f7f2f44d52a6.png">


Follow the same process for remaining two VPC's.

<img width="1503" alt="image" src="https://user-images.githubusercontent.com/74225291/165966751-85e0a4f9-a2a3-4984-acc1-8d55639cd9e0.png">


6. Now will add Route Table entry for all 3 vpc Transit Gateway in respective VPC's private subnet route table.

 <img width="1308" alt="image" src="https://user-images.githubusercontent.com/74225291/165976999-9eac844e-0cde-44b1-a054-b9ad09456818.png">

For now we have added route from VPC1 to VPC2 and in VPC2 to VPC1

<img width="1205" alt="image" src="https://user-images.githubusercontent.com/74225291/165978414-64aa2b01-5a35-41f3-a315-089f87bbb026.png">

Now connect to private EC2 instance in VPC1 using session manager and try to do ssh.
In the initial check I have not added route so it was giving timeout, later I added route then its started working.

<img width="713" alt="image" src="https://user-images.githubusercontent.com/74225291/165985518-164935eb-ddd1-4028-a616-fee47032a397.png">

Currently we dont have route from VPC2 to VPC3 so if we try to do ssh from vpc2 to vpc3 EC2 instance we should get error.

<img width="1240" alt="image" src="https://user-images.githubusercontent.com/74225291/165986783-cfd69abf-59b0-498c-8c97-6283d88d998e.png">


Now add the routes as below for all VPC's.

![image](https://user-images.githubusercontent.com/74225291/165986941-e59d54c7-8390-4f55-b00f-bda0c1301b16.png)


