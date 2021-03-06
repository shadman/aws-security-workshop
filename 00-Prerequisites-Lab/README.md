### Creating an EC2 Key Pair

First we need to create a key pair that will be used to establish an SSH
connection.

1)  Go to the *Key Pairs* in the EC2 instances console

![images](images/1b7a0e08bd10420fa37c1270cffe1f54.png)

2)  Click on the *Create Key Pair* button

![images](images/d3c32b52f680b2710b9bb1a93c1407c1.png)

3)  Key in *TechShift-KeyPair* in the name box.

![images](images/c4490616d6988656078799a2695d6b01.png)

4)  Now you will be able to see the key pair in the console and it will be in your *Downloads* folder.

![images](images/7324683f50d7dbe301fa0c476d84153a.png)

### Create a Cloud9 environment

1) Go to the Cloud9 console and press *Create environment*.

![prerequisites lab](images//1d057a6d465f25b6ff1842ee465ab08d.png)

2) Provide a name for your environment - you can name it _SecurityImmersionDay_

![images/](images/cloud9-environment-name.png)

3) Leave all the parameters untouched and press *Next Steps*.


![images/](images/bd9d46e5b0a0c7f7e0e405566a2a4806.png)


4) Review the settings and press *Create environment*.


![images/](images/09e18a38e2942abbedcfae852c057fb3.png)


5) Now you have an IDE in the cloud.


![images/](images/6bf8fc54f1f01e9eda93a8dc95f5dccd.png)

6) Click on *Open IDE*

7) We will be using Cloudformation to spin up a couple of default resources. Grab the CFN template.

```
wget https://raw.githubusercontent.com/czhc/aws-security-workshop/master/Cloudformation/security-workshop.json

```

![images/](images/clone.png)

8) Once the repository is cloned, deploy the CloudFormation template using the following command:

```sh
aws cloudformation create-stack --template-body file://./security-workshop.json --stack-name securityImmersionDayStack --capabilities CAPABILITY_NAMED_IAM --parameters ParameterKey=InstanceType,ParameterValue=t2.small ParameterKey=KeyName,ParameterValue=SecurityImmersionDay ParameterKey=RDSPassword,ParameterValue=securityID2020 ParameterKey=RDSUsername,ParameterValue=admin ParameterKey=VPCCIDR,ParameterValue=172.4.0.0/16
```

9) Once the installation begins you can check the status of the deployement using this command:

```sh
aws cloudformation describe-stacks --stack-name securityImmersionDayStack \
                                   --query 'Stacks[0].StackStatus' \
                                   --output text
```

![images/](images/statuscheck.png)

 **:heavy_exclamation_mark: DO NOT move past this point until you see CREATE_COMPLETE as the status for your CloudFormation stack**

Explore the output of Stack. What are the resources that were created from the Stack?

```sh
aws cloudformation describe-stack-resources --stack-name securityImmersionDayStack --output table --query "StackResources[].ResourceType"

```

10) Move to the [first lab (CloudTrail)](../01-CloudTrail-Lab/README.md)
