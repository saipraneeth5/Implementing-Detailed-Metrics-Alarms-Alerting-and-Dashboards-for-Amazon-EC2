# Implementing Detailed Metrics Alarms, Alerting, and Dashboards for Amazon EC2

## Prerequisite
- AWS account

## Installing a CloudWatch Agent on EC2 instance
### Steps
- Log in to [AWS console](https://aws.amazon.com/console/).
- Navigate to **EC2** service by using search bar.

    ![EC2_Search](cloudwatch/EC2_Search.png)

- We need an EC2 instance in running state to proceed forward.
    - If you don't have EC2 instance created, create one. [AWS Elastic Cloud Compute](https://kubesimplify.com/aws-elastic-cloud-compute) is a blog, showing how to create a EC2 instance.
    - If you have an EC2 instance, proceed with next steps.

- Navigate to your instance

    ![EC2_Instances](cloudwatch/EC2_Instances.png)

- Now you will see your instance, select your instance and click on **connect**.

    ![EC2_Connect](cloudwatch/EC2_Connect.png)

- Connect to your EC2 instance, using any one method as shown below.
    ![EC2_Connect_Options](cloudwatch/EC2_Connect_Options.png)

- Download and configure **CloudWatch** agent for your selected operating system running in your EC2 instance from [here](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/download-cloudwatch-agent-commandline.html).

- Create a **CloudWatch** configuration file for your EC2 instance. Refer [documentation](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/create-cloudwatch-agent-configuration-file-wizard.html#cloudwatch-agent-running-wizard) for configuring **CloudWatch**.

- **Amazon CloudWatch Agent Configuration Manager** will prompt with below questions, choose the options per your configuration and requirement.

    1. On which OS are you planning to use the agent?
    2. Are you using EC2 or On-Premises hosts?
    3. Which user are you planning to run the agent? - choose **cwagent**.
    4. Do you want to turn on StatsD daemon? - My choice **No**
    5. Do you want to monitor metrics from CollectD? WARNING: CollectD must be installed or the Agent will fail to start - My choice **No**
    6. Do you want to monitor any host metrics? e.g. CPU, memory, etc. - Choose **Yes**
    7. Do you want to monitor cpu metrics per core? - Choose **Yes**
    8. Do you want to add ec2 dimensions (ImageId, InstanceId, InstanceType, AutoScalingGroupName) into all of your metrics if the info is available? - Choose **Yes**
    9.Do you want to aggregate ec2 dimensions (InstanceId)? - Choose **Yes**
    10. Would you like to collect your metrics at high resolution (sub-minute resolution)? This enables sub-minute resolution for all metrics, but you can customize for specific metrics in the output json file.
    11. Which default metrics config do you want? - My choice **Standard**
    12. Are you satisfied with the above config? Note: it can be manually customized after the wizard completes to add additional items.
    13. Do you have any existing CloudWatch Log Agent (http://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/AgentReference.html) configuration file to import for migration? - choose **No**
    14. Do you want to monitor any log files? - My choice **No**
    15. Do you want to store the config in the SSM parameter store? - Choose **No**

- Start **CloudWatch** agent. [Documentation for starting CloudWatch agent](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/install-CloudWatch-Agent-on-EC2-Instance-fleet.html#start-CloudWatch-Agent-EC2-fleet).


## Configuring Metrics with Alarms
### Steps
- Navigate to **Cloudwatch** using search bar

    ![Cloudwatch](cloudwatch/Cloudwatch.png)

- Find and click on **Create Alarm**
- Creating an Alarm
    - Click on **Select Metric**

        ![Cloudwatch_Select_Metric](cloudwatch/Cloudwatch_Select_Metric.png)

    - Under **Custom namespaces** select **CWAgent**

        ![Cloudwatch_CWAgent](cloudwatch/Cloudwatch_CWAgent.png)

    - In **Browse** section, select a card as per your requirement and go through other section and modify per requirement.

        ![Cloudwatch_Select](cloudwatch/Cloudwatch_Select.png)

    - Select appropriate EC2 configuration from displayed list.
    - Modify **Metric** and **Conditions** cards as per your requirement and click on **Next**.

    - In **Notification** card, select **Create new topic** and provide topic name, emails addresses for notifications. Click on **Create topic**. Click **Next**.

        ![Cloudwatch_Notification](cloudwatch/Cloudwatch_Notification.png)

    - Enter Alarm name and description(optional).

        ![Cloudwatch_Alarm](cloudwatch/Cloudwatch_Alarm.png)


## Enabling an Email Notification with the SNS
### Steps
- Navigate to **SNS** using search bar

    ![SNS](cloudwatch/SNS.png)

- From left hand pane, in **Dashboard** find and click **Subscriptions**.

    ![SNS_Subcriptions](cloudwatch/SNS_Subcriptions.png)

- You will be seeing **pending confirmation** in **ID**. Now open your provided email and Search for an email from **no-reply@sns.amazonaws.com** with subject line **AWS Notification - Subscription Confirmation**.  In that email click on **Confirm subscription**.

    - Before clicking **Confirm subscription** in mail. Screen in SNS.

        ![SNS_Pending_Email](cloudwatch/SNS_Pending_Email.png)
    
    - After clicking **Confirm subscription** in mail. Screen in SNS.

        ![SNS_Confirmation_Email](cloudwatch/SNS_Confirmation_Email.png)

## Displaying Metrics in a Dashboard
### Steps
- Navigate to **Cloudwatch** using search bar

    ![Cloudwatch_search](cloudwatch/CloudWatch_Search.png)

- Click on **Dashboard** from left pane and click on **Create dashboard**

    ![Cloudwatch_Create_Dashboard](cloudwatch/Cloudwatch_Create_Dashboard.png)

- Provide dashboard name and click on **Create dashboard**

    ![Cloudwatch_Create_Dashboard_Name](cloudwatch/Cloudwatch_Create_Dashboard_Name.png)

- **Add widget** screen will pops-up. Select your desired type of widget per requirement.
- When **Add to this dashboard** card displayed, click on **Metrics**.
- Select **CWAgent** under **Custom namespaces**.
- In **Browse** section, select a card as per your requirement and go through other section and modify per requirement.

    ![Cloudwatch_Select](cloudwatch/Cloudwatch_Select.png)

- Select appropriate EC2 configuration from displayed list.
- Modify other options if required and click on **Create widget**.
- Create widgets per your requirement by clicking on **Add widget**.
- After creating desired no. of widgets, finally click on **Save dashboard**.

**Viola, reached end of the guide for Implementing Detailed Metrics Alarms, Alerting, and Dashboards for Amazon EC2 is completed.**

**Happy Learning :)**
