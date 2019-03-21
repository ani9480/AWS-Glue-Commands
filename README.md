# AWS-Glue-Commands


1.	Create job:

aws glue create-job --name Any name --role arn:aws:iam::120373437580:role/AIMDataDevExecutionRole --command Name=glueetl,ScriptLocation=s3://lambdas-test/acela_csv_read.py --default-arguments "[{\"--extra-py-files\":\"s3://lambdas-test/library.zip\"}]" --max-retries 0  --allocated-capacity  2 --profile wifidev

aws glue create-job --name Any name --role arn:aws:iam::120373437580:role/AIMDataDevExecutionRole --command Name=glueetl,ScriptLocation=s3://lambdas-test/acela_csv_read.py --default-arguments extrapyfiles=s3://lambdas-test/library.zip --max-retries 0  --allocated-capacity  2 --profile wifidev

2.	Create Trigger:

Scheduled:

aws glue create-trigger --name test.job --type SCHEDULED --schedule "cron(00 19 * * ? *)" –actions JobName=test.icomera_trigger_job_test,Timeout=360,NotificationProperty={NotifyDelayAfter=2} --start-on-creation

With Dependencies:

aws glue create-trigger --name test.job --type CONDITIONAL --predicate Logical="AND",Conditions=[{LogicalOperator="EQUALS",JobName="test.devjob",State="SUCCEEDED"}] --actions JobName=test.dev2job,Timeout=360,NotificationProperty={NotifyDelayAfter=2} --start-on-creation


3.	Start Job:

aws glue start-job-run --job-name Any name --allocated-capacity 2 --profile wifidev

4.	Delete Job:

aws glue delete-job --job-name test.devjob

5.	Delete Trigger

aws glue delete-trigger --name test.devtrigger
