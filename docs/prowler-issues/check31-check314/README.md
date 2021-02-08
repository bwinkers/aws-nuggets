# CIS Level 1 Metrics and Alarms

We assume ConrtolTower hasenabled CloudtrialLogs already.

We will create filter metrics and alarms for each.

```bash
 3.1  [check31] Ensure a log metric filter and alarm exist for unauthorized API calls (Scored)   
       FAIL! CloudWatch group aws-controltower/CloudTrailLogs found but no metric filters or alarms associated 

 3.2  [check32] Ensure a log metric filter and alarm exist for Management Console sign-in without MFA (Scored)   
       FAIL! CloudWatch group aws-controltower/CloudTrailLogs found but no metric filters or alarms associated 

 3.3  [check33] Ensure a log metric filter and alarm exist for usage of root account (Scored)   
       FAIL! CloudWatch group aws-controltower/CloudTrailLogs found but no metric filters or alarms associated 

 3.4  [check34] Ensure a log metric filter and alarm exist for IAM policy changes (Scored)   
       FAIL! CloudWatch group aws-controltower/CloudTrailLogs found but no metric filters or alarms associated 

 3.5  [check35] Ensure a log metric filter and alarm exist for CloudTrail configuration changes (Scored)   
       FAIL! CloudWatch group aws-controltower/CloudTrailLogs found but no metric filters or alarms associated 

 3.8  [check38] Ensure a log metric filter and alarm exist for S3 bucket policy changes (Scored)   
       FAIL! CloudWatch group aws-controltower/CloudTrailLogs found but no metric filters or alarms associated 

 3.12  [check312] Ensure a log metric filter and alarm exist for changes to network gateways (Scored)   
       FAIL! CloudWatch group aws-controltower/CloudTrailLogs found but no metric filters or alarms associated 

 3.13  [check313] Ensure a log metric filter and alarm exist for route table changes (Scored)   
       FAIL! CloudWatch group aws-controltower/CloudTrailLogs found but no metric filters or alarms associated 

 3.14  [check314] Ensure a log metric filter and alarm exist for VPC changes (Scored)   
       FAIL! CloudWatch group aws-controltower/CloudTrailLogs found but no metric filters or alarms associated
```

```bash
aws --profile admin-email \
cloudformation create-stack \
--stack-name cis-alarms \
--template-body file://CloudWatch_Alarms_for_CloudTrail_API_Activity.json \
--parameters ParameterKey=LogGroupName,ParameterValue='aws-controltower/CloudTrailLogs' \
ParameterKey=Email,ParameterValue='bwinkers@gmail.com'
```
