# Getting Started with AWS Auto Scaling

## 1. Create a Launch Configuration

1.1\.	Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

1.2\.	On the navigation pane, under **AUTO SCALING**, choose **Launch Configurations**.

1.3\.	On the next page, choose **Create launch configuration**.

1.4\.	On the Choose AMI page, find an **Amazon Linux 2 AMI (HVM), SSD Volume Type** at the top of the list and choose **Select**.

1.5\.	On the Choose Instance Type page, select a **t2.micro** for your instance. Choose **Next: Configure details**.

1.6\.	On the Configure Details page, do the following:

* For **Name**, type `WebServers` for your launch configuration.
* For **IAM Role**, select **Our_Experiences_S3** to associate with the instances.
* (Optional) By default, basic monitoring is enabled for your Auto Scaling instances. To enable detailed monitoring for your Auto Scaling instances, select **Enable CloudWatch detailed monitoring**.
* Expand the section **Advanced Details**, copy the [content file](scripts/bootstrap-github.sh), from the script replace `<ENDPOINT>` with the RDS instance endpoint and `<BUCKET_NAME>` with your bucket name created earlier, paste it in **User data** as text.

1.7\.	Choose **Next: Add Storage** and **Next: Configure Security Group**.

1.8\.	Select **Select and existing security group** and select **our-experiences**, choose **Review** and for the Warning choose **Continue**.

1.9\.	Choose **Create launch configuration**.

1.10\.	Select the key pair that you created in the beginning of this lab from the drop-down and check the **"I acknowledge"** checkbox. Then choose **Create launch configuration** and **Close**.

## 2. Create an Auto Scaling Group

2.1\.	Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

2.2\.	On the navigation pane, under **AUTO SCALING**, choose **Auto Scaling Groups**.

2.3\.	Choose **Create Auto Scaling group**.

2.4\.	On the **Create Auto Scaling Group** page, choose **Launch Configuration**, choose the existing launch configuration **WebServers**, and then choose **Next Step**.

2.5\.	On the **Configure Auto Scaling group details** page, do the following:

* For **Group name**, type `WebServer` for your Auto Scaling group.
* For **Group size**, type `2` as the initial number of instances for your Auto Scaling group.
* For **Network**, choose **My VPC** for your Auto Scaling group.
* For **Subnet**, select **10.1.2.0/24** (Private Subnet 01) and **10.1.3.0/24** (Private Subnet 02).
* Expand **Advanced Details**, choose **Receive traffic from one or more load balancers**, choose the target group **our-experiences**, for the **Health Check Type** select **ELB** and select **Enable CloudWatch detailed monitoring**.

2.6\.	Choose **Next: Configure scaling policies**.

2.7\.	In **Configure scaling policies** select **Use scaling policies to adjust the capacity of this group**.

2.8\.	Click on **Scale the Auto Scaling group using step or simple scaling policies**.

2.9\.	For **Increase Group Size**, click on **Add new alarm**, select **>=** and type `80` **Percent** and choose **Create Alarm**, take the action **Add** and type `2`.

2.10\.	For **Decrease Group Size**, click on **Add new alarm**, select **<=** and type `40` **Percent** and choose **Create Alarm**, take the action **Remove** and type `2`.

2.11\.	Choose **Review** and **Create Auto Scaling group**.

## 3. Accesing the URL web page

After creating the Auto Scaling group wait about 5 minutes until the web instances come into service.

3.1\.	Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

3.2\.	On the navigation pane, under **LOAD BALANCING**, choose **Load Balancers**.

3.3\.	Select **our-experiences**, from the **Description** section copy the **DNS name**.

3.4\.	Now test in your browser the web page by accessing with the DNS name.