# Lab 4: Creating an Amazon RDS Database

## Lab overview

Traditionally, creating a database can be a complex process that requires either a database administrator or a systems administrator. In the cloud, you can simplify this process by using Amazon Relational Database Service (Amazon RDS).

## Objectives

After completing this lab, you should be able to:

- Launch a database using Amazon RDS
- Configure a web application to connect to the database instance

At the end of this lab, your architecture will look like the following example:

![Architecture Diagram](https://github.com/Sohaib63/AWS-Intro-to-Cloud-Lab-4/blob/main/Lab%20tut%20pic.png)

## Duration

This lab requires approximately 30 minutes to complete.

## Prerequisites

This lab requires:

- Access to a notebook computer with Wi-Fi running Microsoft Windows, macOS, or Linux (Ubuntu, SUSE, or Red Hat)
- For Microsoft Windows users, administrator access to the computer
- An Internet browser such as Chrome or Firefox.

**Note:** This lab is incompatible with Internet Explorer 11. Use a different browser to launch this lab.

## AWS service restrictions

In this lab environment, access to AWS services and service actions might be restricted to only the ones that you need to complete the lab instructions. You might encounter errors if you attempt to access other services or perform actions beyond the ones that this lab describes.

## Accessing the AWS Management Console

1. At the top of these instructions, select **Start Lab** to launch your lab.
2. A Start Lab panel opens displaying the lab status.
3. Wait until you see the message **Lab status: ready**, and then choose the **X** to close the Start Lab panel.
4. At the top of these instructions, choose **AWS**.
5. The AWS Management Console opens in a new browser tab. The system automatically signs you in.

> Tip: If a new browser tab does not open, a banner or icon at the top of your browser typically indicates that your browser is preventing the site from opening pop-up windows. Select the banner or icon, and choose **Allow pop-ups**.

6. Arrange the AWS Management Console tab so that it displays alongside these instructions. Ideally, you should be able to see both browser tabs at the same time to make it easier to follow the lab steps.


## Task 1: Creating an Amazon RDS database

In this task, you create a MySQL database in your virtual private cloud (VPC). MySQL is a popular open-source relational database management system (RDBMS), so there are no software licensing fees.

**Windows Users:** Use Chrome or Firefox as your web browser for this lab. The lab instructions are not compatible with Internet Explorer because of a difference in the Amazon RDS console.

1. On the Services menu, choose RDS.
2. Choose Create database.
3. Under Engine options, select MySQL.
    * The options include several use cases, ranging from enterprise-class databases to Dev/Test systems. In the options, you might notice Amazon Aurora. Aurora is a MySQL-compatible system that was re-architected for the cloud. If your company uses large-scale MySQL or PostgreSQL databases, Aurora can provide enhanced performance.
4. In the Templates section, select Dev/Test.
5. You can now select a database configuration, including software version, instance class, storage, and login settings. The Multi-AZ deployment option automatically creates a replica of the database in a second Availability Zone for high availability.
6. In Availability and durability section, choose Single DB instance.
7. In the Settings section, configure the following options:
    * DB instance identifier: inventory-db
    * Master username: admin
    * Master password: lab-password
    * Confirm password: lab-password
8. In the DB instance class section, configure the following options:
    * Select Burstable classes (includes t classes).
    * Select db.t3.micro.
9. In the Storage section, configure the following options:
    * Storage type: Select General Purpose SSD (gp2).
    * Allocated storage: Enter 20 GiB.
10. In the Connectivity section, configure the following option: 
    * Virtual private cloud (VPC): Lab VPC
11. In the Connectivity section, for Existing VPC security groups, choose the X on default to remove this security group. Then choose the dropdown list, and select DB-SG to add it.
12. Scroll to the Monitoring section, and clear (deselect) the Enable Enhanced monitoring option.
13. Scroll to the Additional configuration section, and choose to expand it. 
14. For Initial database name, enter inventory. This is the logical name of the database that the application will use.
15. You can review the many other options displayed on the page, but leave them set to their default values. Options include automatic backups, the ability to export log files, and automatic version upgrades. The ability to activate these features with check boxes demonstrates the power of using a fully managed database solution instead of installing, backing up, and maintaining the database yourself.
16. At the bottom of the page, choose Create database.
17. You should receive this message: Creating database inventory-db.
    * If you receive an error message that mentions rds-monitoring-role, confirm that you have cleared the Enable Enhanced monitoring option in the previous step, and then try again.
18. Before you continue to the next task, the database instance status must be Available. This process could take several minutes.
![AWS](https://github.com/Sohaib63/AWS-Intro-to-Cloud-Lab-4/blob/main/Screenshot%20(70).png)
## Task 2: Configuring web application communication with a database instance

This lab automatically deployed an Amazon Elastic Compute Cloud (Amazon EC2) instance with a running web application. You must use the IP address of the instance to connect to the application.

1. On the **Services** menu, choose EC2.
2. In the left navigation pane, choose Instances.
3. In the center pane, there should be a running instance that is named **App Server**.
4. Select the check box for the App Server instance.
5. In the **Details** tab, copy the **Public IPv4 address** to your clipboard.

   > **Tip:** If you hover over the IP address, a copy icon appears. To copy the displayed value, choose the icon.

6. Open a new web browser tab, paste the IP address into the address bar, and then press Enter.
7. The web application should appear. It does not display much information because the application is not yet connected to the database.
8. Choose **Settings**.
9. You can now configure the application to use the Amazon RDS database instance that you created earlier. You first retrieve the database endpoint so that the application knows how to connect to a database.
10. Return to the AWS Management Console, but do not close the application tab. (You will return to it soon.)
11. On the **Services** menu, choose RDS.
12. In the left navigation pane, choose Databases.
13. Choose **inventory-db**.
14. Scroll to the **Connectivity & security** section, and copy the **Endpoint** to your clipboard.
    > It should look similar to this example: `inventory-db.crwxbgqad61a.rds.amazonaws.com`

15. Return to the browser tab with the inventory application, and enter the following values:
    - For **Endpoint**, paste the endpoint you copied earlier.
    - For **Database**, enter `inventory`
    - For **Username**, enter `admin`
    - For **Password**, enter `lab-password`
16. Choose **Save**.

    > The application will now connect to the database, load some initial data, and display information.

17. You can use the web application to add inventory, edit, and delete inventory information. The inventory information is stored in the Amazon RDS MySQL database that you created earlier in the lab. This means that in the event of any failure in the application server, you will not lose any data. It also means that multiple application servers can access the same data.
18. Insert new records into the table. Ensure that the table has 5 or more inventory records before submitting your work.
19. You have now successfully launched the application and connected it to the database.
![AWS](https://github.com/Sohaib63/AWS-Intro-to-Cloud-Lab-4/blob/main/Screenshot%20(71).png)
Optional: To access the saved parameters, go to the AWS Management console. On the **Services** menu, choose Systems Manager. In the left navigation menu, choose Parameter Store.

# Submitting your work

At the top of these instructions, choose `Submit` to record your progress, and when prompted, choose `Yes`.
