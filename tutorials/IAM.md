# Getting Started with Amazon IAM

## 1. Create an IAM Role for EC2 Instance

1.1\.	Sign in to the AWS Management Console and open the Amazon S3 console at https://console.aws.amazon.com/iam/.

1.1\.	Choose **Roles** and **Create role**. 

1.3\.	On the **Select type of trusted identity** page, you decide who or what will be able to assume this role. For this lab, we will create a role that allows an EC2 instance to read files in S3. Therefore, we will stay on the **AWS service** tab and select **EC2**. Go to **Next: Permissions**.

1.4\.	Attach a managed policy with S3 Read Only access to the role by typing **s3** into the search bar, and then selecting the **AmazonS3FullAccess** policy. Go to the **Next: Tags** and **Next: Review**.

1.5\.	Give your role a descriptive name, such as `Our_Experiences_S3` and edit the role description to be a helpful summary of what this role is. When you’re done, **Create Role**.