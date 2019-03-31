# Getting Started with Amazon RDS

## 1. Create a Subnet Group

1.1\.	Sign into the AWS Management Console and open the Amazon RDS console at https://console.aws.amazon.com/rds.

1.2\.	Click on **Subnet groups** and click on **Create DB Subnet Group**.

1.3\.	Name your subnet group as `PrivateDBGroup` and a short description.

1.4\.	For the VPC select **My VPC**.

1.5\.	In **Add subnets** section, select the Private Subnets, from **us-east-1a** select **10.1.2.0/24** (Private Subnet 01), choose **Add subnet** and for **us-east-1b** select **10.1.3.0/24** (Private Subnet 02), choose **Add subnet**.

1.6\.	Choose **Create**.

## 2. Launch an RDS Instance

2.1\.	Sign into the AWS Management Console and open the Amazon RDS console at https://console.aws.amazon.com/rds.

2.2\. Click on **Create database** or **Get Started Now**.

2.3\. We will be using a MySQL database, so choose **MySQL** from the available engines.

2.4\. Click **Next**.

2.5\. Check **Production - MySQL** for the Use Case, at the bottom of the page, and then click **Next**.

2.6\. Fill out the DB Instance details with the following information and click **Next**:

•	**DB engine version:** `Use the default engine version`

•	**DB Instance class:** `db.t2.micro`

•	**Storage type:** `General Purpose (SSD)`

•	**Allocated Storage:** `20 GB`

•	**DB instance identifier:** `our-experiences`

•	**Master username:** `awsuser`

•	**Master Password:** `awspassword`

2.7\.	In **Configure Advanced Settings**, fill out Network & Security with the following information:

•	**Virtual Private Cloud (VPC):** `My VPC`

•	**Subnet group:** `privatedbgroup`

•	**Public accessibility:** `No`

•	**Availability zone:** `No Preference`

•	**VPC security groups:** Select **Choose existing VPC security groups**, then pick `our-experiences-db`, remove the default security group.

•	**Database nema:** `our_experiences`.

2.8\.	Choose **Create database** and **View DB Instance details**.

2.9\. From the **Connectivity & security** description, copy the **Endpoint** once is available, you will use it in the next section.

**Note**: This may take up to 5 minutes as the database is being created and backed up, once is available you can continue.

## 3. Creating the database Tables

3.1\. Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

3.2\. In the navigation pane, under **INSTANCES**, choose **Instances**.

3.3\. Connect to your **Bastion** EC2 Instance by SSH.

[Connecting to Your Linux Instance from Windows Using PuTTY](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/putty.html).
[Connecting to Your Linux Instance Using SSH](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html)

3.4\. Execute the following bash commands, change **<ENDPOINT>** with your Endpoint copied.

```bash
sudo su -
export DB_HOST=<ENDPOINT>
export DB_USER=awsuser
export DB_PASSWORD=awspassword
export DB_NAME=our_experiences
wget https://raw.githubusercontent.com/aurbac/laravel-our-experiences/master/scripts/our_experiences.sql
mysql -h$DB_HOST -u$DB_USER -p"$DB_PASSWORD" $DB_NAME < our_experiences.sql 2>/dev/null
```






















