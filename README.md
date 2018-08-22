# SumoLogic-Duo-Lambda-Function
# Log Types
Sumo Logic App for Duo Security uses following logs. 
Authentication Logs
Administrator Logs
Telephony Logs



Step 1. Create hosted collector and HTTP source

In this step you create, on the Sumo service, an HTTP endpoint to receive your logs. This process involves creating an HTTP source on a hosted collector in Sumo. In Sumo, collectors use sources to receive data.
To create a hosted collector and an HTTP source
If you don’t already have a Sumo account, you can create one by clicking the Free Trial button on https://www.sumologic.com/.
Create a hosted collector, following the instructions on Configure a Hosted Collector in Sumo help. (If you already have a Sumo hosted collector that you want to use, skip this step.)
Create an HTTP source on the collector you created in the previous step. For instructions, see HTTP Logs and Metrics Source in Sumo help.
When you have configured the HTTP source, Sumo will display the URL of the HTTP endpoint. Make a note of the URL. You will use it when you configure the Lambda Function to send data to Sumo.

Step 2.  Download Lambda Function code and Import it to AWS Lambda

Download the zip file from here. 
Or 
You can clone the github repository, and zip the files (duo_client folder and lambda_function.py). Feel free to submit PRs for any enhancements/suggestions.

Login to AWS console, navigate to Lambda service
Click Create Function
Provide Name, Run Time as Python 3.6
Choose existing Role, or create new one to execute Lambda function
Click Create Function
At Function Code section of next page, select Upload a Zip File from Code entry type. Upload the zip file you downloaded. 

Click Save.
Function directory structure should look like this, make sure there is no extra folder in there between root folder (duo_test2) and duo_client folder and lambda_function.py is directly under root folder


Step 3. Define Environment Variables for Lambda Function.  
Define following environment variables at AWS Lambda Function page
COLL_ENDPOINT : Sumo Logic Hosted Collector End Point
I_KEY
S_KEY
HOST 
I_KEY, S_KEY, and HOST are Duo’s integration key, secret key, and API hostname. For more info 

SCAN_INTERVAL_IN_SEC : Polling interval for Duo APIs. Recommended value is 600 secs [10 mins].


Step 4. Add Timer trigger for Lambda Function you just created  
Create a rule to run your Lambda function on a schedule.
To create a rule using the console
Open the CloudWatch console at https://console.aws.amazon.com/cloudwatch/.
In the navigation pane, choose Events, Create rule.
For Event Source, do the following:
Choose Schedule.
Choose Fixed rate of and specify the schedule interval for 10 minutes
For Targets, choose Add target and then choose Lambda function.
For Function, select the Lambda function that you created.
Choose Configure details.
For Rule definition, type a name and description for the rule.
Choose Create rule.

