# transite-gateway
transite-gateway

Without Transit Gateway

![image](https://user-images.githubusercontent.com/74225291/165943139-c2c443d0-a4df-43e4-a6c4-86108c52d168.png)


With Transit Gateway

![image](https://user-images.githubusercontent.com/74225291/165943351-f6f7aca7-e879-4d66-b7f0-17c3cc7c6950.png)

Routing Sample:

![image](https://user-images.githubusercontent.com/74225291/165943418-c30948dc-a198-4cbb-82b0-9ed13c5be8c9.png)


Here we are doing the setup of Transite gateway on same aws account across three diffrent VPC's.

Demo Setup:

			
			|		|VPC1		|VPC2		|VPC3		|
			|		|===============|===============|===============|
			|CIDR		|10.1.0.0/16	|10.2.0.0/16	|10.3.0.0/16	|
			|Public Subnet	|10.1.0.0/20	|10.2.0.0/20	|10.3.0.0/20	|
			|Private Subnet	|10.1.10.0/24	|10.2.10.0/24	|10.3.10.0/24	|
			

<img width="396" alt="image" src="https://user-images.githubusercontent.com/74225291/165944695-5c42ceba-0c20-4802-9e7f-f8488e0e9ee3.png">




VPC1 : 10.1.0.0/20
CIDR
Public Subnet. :
Private Subnet :
VPC2 : 10.2.0.0/20


VPC3 : 10.3.0.0/20
