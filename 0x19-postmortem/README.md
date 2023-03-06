# 0x19-postmortem

# Issue Summary
 On 02/03/2023 From 9:15 AM to 10:00 AM EAT all requests for the homepage to our servers got a 404 response error affecting 100% of the users.

# Timeline
9:10 AM : Updates push

9:15 AM : Noticing the problem

9:15 AM : Notifying the both front end and backend teams

9:20 AM : Successful change rollback

9:24 AM : Server Restarts begin

9:27 AM : 100% of traffic back online

9:30 AM : start debugging the push with the problem

9:50 AM : Probelm fixed and pushed the changes

9:55 AM : Server restart begins

10:00 AM : 100% traffic back online with the new updates
# Root cause and resolution
After rolling back changes we knew that the changes were made by the front end team so we took the broken changes and run them on a test server which replicated same problem, our server uses apache2 and apache2 error logs didn't give enough infomation about the problem so we traced the apache2 process using strace and when a request is sent strace tool catchs a lot of error and after some scaning foR these errors we found the error which is a typo in page file extention 
# Corrective and preventative measures
To prevent similar problems from happening again we will

Create an automated test pipeline for every update push
Add a monitoring software to our servers which will monitor lot of things and one of them Network Traffic resquests and responses and configure it to make an lert to the teams when too much non desired responses were sent like 404
Create a tests for every new update and the teams should not push until those tests pass