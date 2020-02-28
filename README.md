# Example Cloud Formation

This example shows how to create diferent stacks (VPC, EC2, RDS) and in the main yml file make the references.

## VPC yml file

This yml file creates a VPC with diferents resources ( 3 Public Subnets, 3 Private Subnets, DMZ Security Group, RDS Security Group, Nat Gateway and Internet Gateway) and the outputs will be used for EC2 and RDS.

### Parameters

* EnvironmentName: An environment name that is prefixed to resource names
* VpcCIDR: The IP range (CIDR notation) for this VPC
* PublicSubnet1CIDR: The IP range (CIDR notation) for the public subnet in the first Availability Zone
* PublicSubnet2CIDR: The IP range (CIDR notation) for the public subnet in the second Availability Zone
* PublicSubnet3CIDR: The IP range (CIDR notation) for the public subnet in the third Availability Zone
* PrivateSubnet1CIDR: The IP range (CIDR notation) for the private subnet in the first Availability Zone
* PrivateSubnet2CIDR: The IP range (CIDR notation) for the private subnet in the second Availability Zone
* PrivateSubnet3CIDR: The IP range (CIDR notation) for the private subnet in the third Availability Zone

## RDS Yml File

This yml file creates a RDS in a private network and in a security group. The private subnets and the securiry Group are obtained from the VPC.

### Parameters

* DBType: The name of the database engine that you want to use for this DB instance. (Mysql, Oracle, AuroraDB, Sql Server, etc)
* DBVersion: The version number of the database engine to use.
* DBInstanceID: Name for the DB instance
* DBName: Name for the Database
* DBInstanceClass: Power and memory requeriments
* DBAllocatedStorage: Storage (GiB)
* DBUsername: Username for the database
* DBPassword: Password for the database
* VPCSecurityGroup: Vpc security group for the database (Obtain from VPC OutPuts)
* PrivateSubnets: Subnets privates list (Obtain from VPC OutPuts)


## EC2 (WordPress) Yml File

This YML file creates a web server with the latest version of WordPress. WordPress automatically connects with RDS.

### Parameters

* Ami: The ID of the AMI.
* EC2InstanceType: Instance Type
* EC2KeyName: Key for access ssh
* EC2Name: Name for the ec2 instance
* DBName: Name for the Database (Obtain from RDS OutPuts)
* DBUsername: Username for the database (Obtain from RDS OutPuts)
* DBPassword: Password for the database (Obtain from RDS OutPuts)
* DBEndPoint: Database Host (Obtain from RDS OutPuts)
* EC2SecurityGroup: Vpc security group for the DMZ (Obtain from VPC OutPuts)
* EC2SubnetId: Subnet public Id (Obtain from VPC OutPuts)

## Main Yml File

This YML file calls the previous stacks and builds the complete architecture.

![alt text](https://drive.google.com/file/d/1aUolKpS_M7Bs6b9SkD1BT14IJzlWllf2/view?usp=sharing)

### Deployment

The yml files of RDS, Ec2 and VPC should be stored in an S3. Only the main yml should be executed in cloudFormation.
 
## Authors

* **Luis Sic** - *Tecnologia Transaccional* - [sluis117](https://github.com/LuisSic)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details
