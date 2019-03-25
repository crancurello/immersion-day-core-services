# Getting Started with Application Load Balancer

## 1. Create the Application Load Balancer for the Backend

1.1\. Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

1.2\. In the navigation pane, under **LOAD BALANCING**, choose **Load Balancers**.

1.3\. Choose **Create Load Balancer**.

1.4\. On the **Select load balancer type** page, choose **Application Load Balancer** and then choose **Create**.

1.5\. Complete the **Configure Load Balancer** page as follows:

  a\. For **Name**, type `our-experiences` for your load balancer.

  b\. For **Scheme**, use an internet-facing load balancer routes requests from clients over the internet to targets.

  c\. For **IP address type**, choose ipv4 to support IPv4 addresses only or dualstack to support both IPv4 and IPv6 addresses.

  d\. For **Listeners**, the default is a listener that accepts HTTP traffic on port 80.

  e\. For **VPC**, select the `My VPC`.

  f\. For **Availability Zones**, select the check box for the Availability Zones to enable for your load balancer. For us-east-1a select the **Public Subnet 01** and for us-east-1b select **Public Subnet 02**.

![Configure Load Balancer](../images/alb.png)

1.6\. Choose **Next: Configure Security Settings** and choose **Next: Configure Security Groups**.

1.7\. Select the existing security group **our-experiences-alb** and choose **Next: Configure Routing**.

1.8\. In the **Configure Routing** section, for **Name** type `our-experiences`, for Target type choose **Instance**.

1.8\. Expand **Advanced health check settings** section, for **Healthy threshold** type `2`.

1.9\. Choose **Next: Register Targets**.

1.10\. Choose **Next: Review**, click on **Create** and **Close**.