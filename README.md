# Create an internet proxy server (squid) by Amazon AWS Cloudformation service.

## Introduction
This template allows AWS customers to launch a Squid server in arbitrary region without loggin in to EC2 servers nor executing any command, but putting the template to [AWS CloudFormation](http://aws.amazon.com/cloudformation/).

This project is rather a proof of concept, but I think some people find this template useful in some use cases. Some oline services restrict the range of source IPs, but people can quickly launch a web proxy in the US, Ireland, Singapore and Japan with this template. People with such demand may not have good technical skill to log in to Linux instances and then install and configure Squid to achieve their goal.

## How to Deploy
0. Create an AWS account, if you don't have one. You need credit card to apply an AWS Account.
1. Save the template to your PC/Mac.
2. Login to the AWS Management Console and open the CloudFormation tab.
3. Choose one of the AWS regions where you want to launch a proxy server and then hit "Create New Stack" button.
4. In "SELECT TEMPLATE": Select "*Upload a Template File*" and point to the template file that you save in step 1. You can leave the other fields as they are, but make sure to type in the *Stack Name* field with any name you feel comfortable.
5. The next page, "SPECIFY PARAMETERS" asks for template-specific information. With EC2 Easy Proxy, you need to specify the port number you would like to use and your client IP address. This template create a firewall called Security Group to restrict other users from using your proxy server. You can check your own IP address [here](http://whatismyipaddress.com/).
   Note that IP address needs to be specified with subnet mask. In other words, if you want to specify only one IP address ("1.2.3.4"), then the field should be "1.2.3.4/32"
   ***If you are fine for any IPs, use "0.0.0.0/0". But you will take the risk to share it to others and cost may generate unexpectly.***
6. Click Continue twice and finish the wizard.
7. When the status of your stack turns green (CREATE_COMPLETE), then click the outputs tab of the bottom pane of the Management Console to find the IP address of the proxy server.
8. Configure your web browser to use the proxy. Enjoy!

**Don't forget to "Delete Stack" and make sure that your instance is terminated when you no longer need the proxy server you launched with this template.**

**Stop the ec2 instance, if you needn't access internet via this proxy server, it will save your money. You can start it later, but with different IP address. You need adjust the IP address in your browser.**

For newer users, please note that AWS free tier allows users to launch a t1.micro instance with an EBS volume as its root device for the first 12 months after the account created.

## Interested in CloudFormation?
For those who are interested in AWS CloudFormation, please visit the following sites for more information:

*   [AWS CloudFormation - product site](http://aws.amazon.com/cloudformation/)
*   [Sample Templates](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/sample-templates-services-us-west-2.html)
*   [AWS CloudFormation Documentation](http://aws.amazon.com/documentation/cloudformation/)
