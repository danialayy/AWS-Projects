Project Objectives:
* To deploy a static website on S3
* To ensure the website is secure, reliable, and easily maintainable.
* To optimise hosting costs by leveraging Amazon S3's efficiency and scalability.




In this project you are going to host a static website on S3/
Note: Static website is a collection of web pages whose content is stable and remains the same for every user.
Every web page on a static website is developed as a single HTML file. Upon request from the visitor, the content is delivered from the server to the web page exactly as it is.
This content does not change unless the original HTML file is edited at the code level. Static websites can be updated manually page by page only. Every visitor receives and views the same content.

A static website is identified as the most suitable solution for this purpose due to its simplicity, reliability, and ease of maintenance.
Consider: Amazon S3 is a scalable object storage service that allows users to store and retrieve any amount of data from anywhere on the web.
Initially designed for data storage, S3 has evolved to become an excellent option for hosting static websites.
A website can also be hosted in the EC2 service, but S3 scores over EC2 service for its pay-as-you-go pricing model and cost effectiveness making it an attractive choice for businesses and developers.
Let's start now!
Task 1: Website Content Preparation
STEP 1: Download website template for EpicReads

Click on the link TemplateMo to download free website templates.

Scrolling down, choose any one of the templates for EpicReads and click on it. (Figure 9.1: Website template)


￼
Figure 9.1: Website template

Scroll down to the bottom of the page and click on the Download button.(Figure 9.2: Template Download)

￼
Figure 9.2: Template Download
STEP 2: Locate the downloaded file in your terminal

Open your terminal, check for the downloaded file with command given below (Figure 9.3: Locate the downloaded file)

? Command: ls

￼
Figure 9.3: Locate the downloaded file


Task 2: Create a new Amazon S3 bucket for hosting the EpicReads website.
STEP 3: Create Amazon S3 bucket

In your terminal use the command below to see the list of buckets you have created in S3
? Command: aws s3 ls
✅ Expected Output: It would give list of buckets created else it would go to the next command line.
Now use the below command to create the command
? Command: aws s3 mb s3://epicreads
? Note: Refer the link to know the guidelines for naming the bucket
✅ Expected Output: make_bucket: epicreads (Figure 9.4: Create bucket)

￼
Figure 9.4: Create bucket
STEP 4: Edit static website hosting

Navigate back to S3 bucket from your console (Figure 9.10: Navigate to S3 bucket)


￼
Figure 9.10: Navigate to S3 bucket

You will find the bucket that has been created, click on the bucket name epicread (Figure 9.11: epicreads bucket)


￼
Figure 9.11: epicreads bucket

As you click you will find there is nothing in the Objects’ section (Figure 9.12: EpicReads Objects).


￼
Figure 9.12: EpicReads Objects

Choose Properties and scroll down to the option Static website hosting and click on Edit button. ( Figure 9.13: Static website hosting)


￼
Figure 9.13: Static website hosting

Click on Enable radio button, choose Host a static website for the option
Hosting Type.

To specify the home or default page of the website, copy paste ‘index.html’ in the download folder from the terminal to the index document option in Properties (Figure 9.14: index.html)


￼
Figure 9.14: index.html

When the webpage faces an error, give 404.html to display the error page and click on Save changes button (Figure 9.15: Edit static web hosting)

￼
Figure 9.15: Edit static web hosting

You will find the success message on top. Scrolling down to the Static website hosting section you will find the link of you bucket, click on it to open the link (Figure 9.16: Static website link)


￼
Figure 9.16: Static website link


STEP 5: Edit bucket settings

Now you will find webpage 403 Forbidden (Figure 9.17: 403 Forbidden)


￼
Figure 9.17: 403 Forbidden
? Note: By default you create any bucket, it is not publicly accessible.
To make the bucket accessible, click on Permissions and you will find that Block all public access is ON. Click on Edit button (Figure 9.18: Bucket settings)

￼
Figure 9.18:Bucket settings
Uncheck the checkbox Block all public access, click on Save changes,type confirm and click on Confirm button (Figure 9.19: Unblock public access)

￼
Figure 9.19: Unblock public access
Clicking once again the bucket link you will the same 403 Forbidden page (Figure 9.20: Bucket link)

￼
Figure 9.20: Bucket link
Once again you will find the same 403 Forbidden page (Figure 9.20: Forbidden page)

￼
Figure 9.20: Forbidden page
? Note: The best part of S3 is that it gives multiple level of blocking to make your bucket public both bucket level and account level.
STEP 6: Add Bucket policy
Here let’s edit the bucket policy so that the bucket is accessible. Under Permissions, scroll down to the Bucket policy and click on the Edit button
(Figure 9.21: Edit Bucket policy)



￼
Figure 9.21: Edit Bucket policy

Copy paste the below script and replace the Bucket-Name with ‘epicreads’ and click on Save changes (Figure 9.22: Bucket Policy)

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": [
        "s3:GetObject"
      ],
      "Resource": [
        "arn:aws:s3:::Bucket-Name/*"
      ]
    }
  ]
}


￼
Figure 9.22: Bucket Policy

? Consider: If you notice the Action: "s3:GetObject" allows the action of retrieving (reading) objects from the bucket, means the users can only see, read the data and can never ever attempt to delete the data.
Now you will find that your S3 bucket is Publicly accessible (Figure 9.23: Publicly accessible)

￼
Figure 9.23: Publicly accessible
Now Click on Properties, scroll down and click on the S3 bucket link that is in Static website hosting section (Figure 9.24: S3 bucket link)

￼
Figure 9.24: S3 bucket link
The link displays 404 Not Found, with message Code: NoSuchKey and the key mentioned there was Key: index.html
? Consider: Navigating back to the epicreads S3 bucket you will find there is no object that has to be uploaded. Well that is the reason it displays 404 Not Found (Figure 9.25: 404 Not Found)

￼
Figure 9.25: 404 Not Found
Task 3: Add files to epicreads S3
STEP 7: Display error page

Let’s make an error file, so that in case the user could not access any of our files and it would look way better than just a 404 Not Found.

Open the terminal and use the command given below (Figure 9.26: vi 404 command)

? Command: vi 404.html

￼
Figure 9.26: vi 404 command
Editor will be opened where you can customise your page with the message as given below and type :wq to save the editor and enter. (Figure 9.27: vi editor)
Hi I am an error page!
Sorry, I will be back soon!

￼
Figure 9.27: vi editor
Use the command given below to list out the files

? Command: ls
You will find out 404.html that we created. Now copy this 404.html file to the epicreads S3 bucket using the command given below (Figure 9.28: Copy error file to S3)

? Command: aws s3 cp 404.html s3://epicreads

￼
Figure 9.28: Copy error file to S3
Refreshing the browser you will find the customised message instead of 404 Not found (Figure 9.29: error page)

￼
Figure 9.29: error page
? Consider: In the other way to understand, this link displays error page as there is no other files available in the bucket for the user to access.
STEP 8: Sync the files to S3 bucket
With no delay let’s upload the files to the S3 Bucket by using the command that is given below

? Command: aws s3 sync . s3://epicreads
? Note:
sync: This is the command used for synchronising directories and objects to Amazon S3.
. : Represents the source directory on your local machine. In this case, it's the current directory (where you are running the command).
s3://epicreads: Specifies the destination S3 bucket where you want to sync the files.
✅ Expected Output: Navigate back to the epicreads S3 bucket in the AWS Management Console and you can see all the files have been uploaded (Figure 9.30: Objects in S3)

￼
Figure 9.30: Objects in S3

Now click refresh in your browser and you should see the Static website is ready ( Figure 9.31: EpicReads Static website)
Task 4: Test run the static website

As the files have been uploaded, all set to give a test run now!
STEP 9: Refresh the browser
Now click refresh in your browser and you should see the Static website is ready (Figure 9.31: EpicReads Static website)

￼
Figure 9.31: EpicReads Static website
Task 5: Monitoring and Maintenance
? Consider: Implementing monitoring tools is essential for tracking website availability, performance, and identifying potential errors.

? Note: AWS provides various services and integrations that can help you achieve comprehensive monitoring. Here's a general guide using Amazon CloudFront and AWS WAF Logs

If you use Amazon CloudFront with AWS WAF, monitor CloudFront access logs and WAF logs to identify potential security threats and track the performance of your CDN.

STEP 10: Configure CloudFront
Navigate to CloudFront from the AWS Console (Figure 9.32: Navigate to CloudFront)


￼
Figure 9.32: Navigate to CloudFront

Click on Create distribution (Figure 9.33: Create distribution)


￼
Figure 9.33: Create distribution

Under Origin Options, Origin domain must be given. For this you must copy paste the link of EpicReads S3 bucket from the browser to the Origin domain. So any requests happen it will be directed to the link in the browser (Figure 9.34:Origin domain)


￼
Figure 9.34:Origin domain



￼
Figure 9.35: Origin
? Consider: If you can see (Figure 9.34:Origin domain) it shows caution that the link is ⚠️Not Secure. Hence it is good to replace it with https.
Scrolling down to the option Default cache behaviour, choose the radio button of Redirect HTTP to HTTPS (Figure 9.36: Default cache behaviour)

￼
Figure 9.36: Default cache behaviour

To configure WAF, scroll down to Web Application Firewall and click on the radio button Enable security protections (Figure 9.37: Configure WAF)

￼
Figure 9.37: Configure WAF

? Note: This service is chargeable as you use Free Tier make sure you delete the service after completing this project.
ℹ️ Learn More: Click here to delete the service

Scroll down and click on the button Create distribution. You will get a success message on top that New Distribution created.
Copy the Distribution domain name and paste in the new browser (Figure 9.38: New Distribution created )

￼
Figure 9.38: New Distribution created
? Note: It takes quiet time for the deployment until then you will be able to see that This site can’t be reached prompt. Giving it sometime, do refresh the browser you will be able to access the same EpicReads static website.(Figure 9.39: EpicReads Static Website)

￼
Figure 9.39: EpicReads Static Website
Congrats you have successfully completed Project 9!

STEP 11: Clean up

⚠️ Caution: Make sure that you clean all the resources that have been created. As you use Free-tier once after your study exploration, clean up all the resources to avoid the charges.
COMMON ERROR - Explanation
ERROR : I'm using the Amazon S3 static website feature but getting an Access Denied error

If you're trying to host a static website using Amazon S3, but you're getting an Access Denied error, check the following requirements:
* Objects in the bucket must be publicly accessible
S3 static website endpoint supports only publicly accessible content. To verify whether an object in your S3 bucket is publicly accessible, open the object's URL in a web browser. Or, you can run a cURL command on the URL.
? Command: http://doc-example-bucket.s3-website-us-east-1.amazonaws.com/index.html
If an Access Denied error is returned by the web browser or cURL command, then the object isn't publicly accessible. To allow public read access to your S3 object, create a bucket policy that allows public read access for all objects in the bucket.

* S3 bucket policy must allow access to the s3:GetObject action
Review your bucket policy, and make sure that there aren't any deny statements that block public read access to the s3:GetObject action.
* The AWS account that owns the bucket must also own the object
To allow public read access to objects, the AWS account that owns the bucket must also own the objects. A bucket or object is owned by the account of the AWS Identity and Access Management (IAM) identity that created the bucket or object.
Note: The object-ownership requirement applies to public read access granted by a bucket policy. It doesn't apply to public read access granted by the object's access control list (ACL).
ℹ️ Learn More: To know more about this click here

* Objects that are requested must exist in the S3 bucket
If the user performing the request doesn’t have s3:ListBucket permissions, then the user gets an Access Denied error for missing objects.
You can run the head-object AWS CLI command to check if an object exists in the bucket.
Note: S3 object names are case-sensitive. If the request doesn't have a valid object name, then Amazon S3 will report that the object is missing.
If the object exists in the bucket, then the Access Denied error isn't masking a 404 Not Found error. Verify other configuration requirements to resolve the Access Denied error.
If the object doesn't exist in the bucket, then the Access Denied error is masking a 404 Not Found error. Resolve the issue related to the missing object.

* Amazon S3 Block Public Access must be disabled on the bucket and account level
Amazon S3 Block Public Access settings can apply to individual buckets or AWS accounts. Confirm that there aren't any Amazon S3 Block Public Access settings applied to either your S3 bucket or AWS account. These settings can override permissions that allow public read access.
ℹ️ Learn More: To know more click here

CONCLUSION
Hosting a static website on AWS provides a powerful and flexible solution, combining storage, content delivery, DNS, and security services to deliver a reliable and high-performance web experience.
By following the steps outlined in this blog, individuals and businesses can establish and maintain a cost-effective and scalable web presence on AWS.
AWS offers a comprehensive set of services that, when combined strategically, provide an optimal environment for hosting static websites. Whether you're a beginner or an experienced developer, AWS's user-friendly interfaces and extensive documentation make the process accessible to all. Embracing AWS for static website hosting opens the door to a world of possibilities for seamless, secure, and scalable web experiences.

How would you ensure the security of a static website hosted on Amazon S3?
To ensure security for a static website hosted on S3, I would take the following steps:
* Enable bucket versioning to protect against accidental data loss.
* Use IAM policies and bucket access control lists (ACLs) to restrict access and ensure only authorized users can modify or delete files.
* Use Amazon CloudFront (a content delivery network) for SSL encryption to provide HTTPS access, ensuring secure communication between clients and the website.
* Enable S3 bucket encryption to protect the data stored in S3 (both in transit and at rest).
* Enable logging on the S3 bucket for access logging to monitor and audit requests to the website.
* Set up a Web Application Firewall (WAF) using AWS WAF to protect against common web exploits.
What are the benefits of using S3 for static website hosting compared to traditional web hosting?
1. Scalability: S3 can automatically scale to handle an increase in traffic without needing to worry about provisioning and managing servers.
2. High Availability and Durability: S3 offers 99.99% uptime and 99.999999999% durability, ensuring your content is always available.
3. Cost-Effective: S3's pay-as-you-go pricing model is much more cost-effective than traditional web hosting services, as you only pay for storage and data transfer.
4. Simple Management: S3 eliminates the need for server maintenance, security patches, and manual scaling.
5. Global Reach: Using Amazon CloudFront alongside S3 allows content delivery from edge locations, improving load times globally.
How would you monitor the performance and availability of the website on S3?
To monitor the performance and availability of the static website hosted on S3, I would use:
* Amazon CloudWatch: Set up custom metrics to monitor the health of the S3 bucket and its usage (e.g., storage size, request count, and error rates).
* CloudFront logs: If CloudFront is used as a CDN, enable logging to analyze website traffic and performance issues.
* S3 Access Logs: Enable S3 access logging to track the number of requests made to the website, identify any 4xx/5xx errors, and monitor traffic patterns.
* Route 53 Health Checks: Use Route 53 to monitor the availability of the S3 bucket endpoint and ensure it’s accessible to users.
* AWS Lambda and CloudWatch Alarms: Set up automated alerts when certain thresholds are reached (e.g., a spike in error rates or unusually high traffic).
What are the cost considerations when hosting a static website on S3, and how would you optimize for cost?
Key cost considerations when hosting a static website on S3 include:
* Storage Costs: S3 charges based on the amount of data stored, so reducing the size of images and media files can help minimize costs.
* Data Transfer Costs: S3 charges for data transferred out of the bucket. To reduce costs, use Amazon CloudFront to cache content at edge locations, which reduces the number of direct requests to S3.
* Request Costs: S3 charges for requests (PUT, GET, LIST, etc.), so minimizing the frequency of requests and optimizing caching strategies can lower costs.
* S3 Storage Class: Use the most cost-effective S3 storage class (e.g., Standard for frequently accessed data or Glacier for infrequently accessed data).
* S3 Lifecycle Policies: Set policies to move or delete outdated content (e.g., using S3 Glacier for old data or automatic deletion of expired content) to reduce storage costs.
* CloudFront Integration: Use CloudFront to cache content at edge locations and reduce S3 data transfer costs, especially for static content like images, CSS, and JavaScript files.




