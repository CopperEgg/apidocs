---
layout: default
title: AWS Accounts
---

## Overview

Each of the API commands described here relate to retrieving, adding and deleting one or more AWS Accounts being monitored at your site.
Each AWS Account is completely described by a Hash.

### The AWS Accounts Hash

An example JSON-encoded AWS Accounts Hash is shown below:

{% highlight ruby %}
{
    "id":1,                                     # AWS Account ID(Assigned by Uptime Cloud Monitor)
    "account_number":"123456789012",            # 12 digit AWS Account Number of account to be monitored
    "access_key_id":"dummy_access_key",         # Internal use only
    "secret_access_key":"dummy_secret_key",     # Internal use only
    "aws_role_arn":"role_arn",                  # Role ARN of AWS role created for monitoring
    "aws_external_id":"4iU9KSyMMbRJ",           # Used for authentication with AWS
    "label":"AWS",                              # Label of AWS Account to show on Uptime Cloud Monitor UI
    "tags":[],                                  # Tags associated with this AWS account
    "discovery_enabled":true,                   # No longer used
    "reading_enabled":true,                     # If account monitoring is enabled
    "last_watched_at":1483697680,               # Internal use only
    "last_cloudtrail_scan_at":null,             # Internal use only
    "monitored_ec2_count":0,                    # EC2 Instances with UCM Server Monitoring enabled
    "unmonitored_ec2_count":95,                 # EC2 Instances without UCM Server monitoring
    "billing":0.0,                              # AWS Account billing
    "created_at":1483682913,                    # Monitoring Added at
    "updated_at":1483699106,                    # Updated monitoring account details last time
    "api_count":5712,                           # Number of times data fetched from cloudwatch
    "previous_month_api_count":0,               # Number of times data fetched from cloudwatch last month
    "include_tags":"",                          # Internal use only
    "exclude_tags":"",                          # Internal use only
    "payer_account":true                        # Account is payer or not
}
{% endhighlight %}

------

## Index

Retrieve a list of all of your AWS Accounts.

#### CURL Command, and variations:
{% highlight sh %}
curl -su <APIKEY>:U https://api.copperegg.com/v2/amazon_accounts.json

curl -s https://<APIKEY>:U@api.copperegg.com/v2/amazon_accounts.json
{% endhighlight %}


#### CURL Response:
Response is a JSON-encoded list of AWS Account Hashes.

{% highlight ruby %}
[
    {
        "id":1,
        "account_number":"123456789012",
        "access_key_id":"dummy_access_key",
        "secret_access_key":"dummy_secret_key",
        "aws_role_arn":"arn:aws:iam::123456789012:role/ucm",
        "aws_external_id":"4iU9KSyMMbRJ",
        "label":"AWS",
        "tags":[],
        "discovery_enabled":true,
        "reading_enabled":true,
        "last_watched_at":1483697680,
        "last_cloudtrail_scan_at":null,
        "monitored_ec2_count":0,
        "unmonitored_ec2_count":95,
        "billing":0.0,
        "created_at":1483682913,
        "updated_at":1483699106,
        "api_count":5712,
        "previous_month_api_count":0,
        "include_tags":"",
        "exclude_tags":"",
        "payer_account":true
    }
]
{% endhighlight %}

------

## Create

Add a new AWS Account.

#### Required parameters:

aws_role_arn
: Role ARN of role created for cross-account access using UCM policy'

aws_external_id
: External ID is a random string used in AWS role creation

account_number
: AWS Account Number which is to be monitored. It must be unique

label
: Label is a String to be shown on UI

#### Optional parameters:

tags
: Tags to apply to this AWS Account, If not specified no tags will be applied.

### Create Example 1: create a new probe using only the required parameters, to demonstrate defaults.

##### Uptime Cloud Monitor needs read-only access through an AWS Role

#### 1) Create a Read-Only Role for Cross-Account Access using -
{% highlight sh %}
Amazon Account Id: 193951620307
External ID: <random string>  # remember for further use
policy -
{ "Version": "2012-10-17", "Statement": [ { "Action": [ "S3:ListBucket", "S3:GetObject" ], "Effect": "Allow", "Resource": "arn:aws:s3:::Cloudtrail*" }, { "Action": [ "cloudwatch:Describe*", "cloudwatch:Get*", "cloudwatch:List*", "cloudsearch:Describe*", "cloudsearch:Get*", "cloudsearch:List*", "dynamodb:DescribeTable", "dynamodb:ListTables", "ec2:Describe*", "elasticache:Describe*", "elasticache:List*", "iam:List*", "iam:Get*", "redshift:Describe*", "rds:Describe*", "rds:ListTagsForResource", "swf:List*", "swf:Describe*", "cloudtrail:DescribeTrails", "cloudtrail:GetTrailStatus", "autoscaling:Describe*", "autoscaling:List*", "autoscaling:Get*", "elasticloadbalancing:Describe*", "s3:Get*", "s3:List*", "sqs:Get*", "sqs:List*", "route53:Get*", "route53:List*", "opsworks:Describe*", "opsworks:Get*", "elasticbeanstalk:List*", "elasticbeanstalk:Describe*", "cloudfront:List*", "cloudfront:Get*", "kinesis:Describe*", "kinesis:Get*", "kinesis:List*", "machinelearning:Describe*", "machinelearning:Get*", "elasticmapreduce:Describe*", "elasticmapreduce:List*", "sns:Get*", "sns:List*", "storagegateway:Describe*", "storagegateway:List*", "workspaces:Describe*" ], "Effect": "Allow", "Resource": "*" } ] }
{% endhighlight %}

#### 2) Check permissions
{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/permission/check.json -d '{ "aws_role_arn":"<Role ARN>","aws_external_id":"<External ID>" }'
{% endhighlight %}
For a permitted AWS account response will be like -
{% highlight sh %}
{"valid":true}
{% endhighlight %}
If response is not similar to above response then retry step-1

#### 3) Add AWS Account

##### Curl Command
{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/amazon_accounts.json -d '{ "aws_role_arn":"<Role ARN>","aws_external_id":"<External ID>","account_number":"<AWS Account Number>","label":"<LABEL>","tags":["<tag1>", "<tag2>"] }'
{% endhighlight %}

##### Curl Response
{% highlight ruby %}
{
    "id":1,
    "account_number":"<Account Number>",
    "access_key_id":"dummy_access_key",
    "secret_access_key":"dummy_secret_key",
    "aws_role_arn":"<Role ARN>",
    "aws_external_id":"<External ID>",
    "label":"<LABEL>",
    "tags":["<tag1>","<tag2>"],
    "discovery_enabled":true,
    "reading_enabled":true,
    "last_watched_at":null,
    "last_cloudtrail_scan_at":null,
    "monitored_ec2_count":0,
    "unmonitored_ec2_count":0,
    "billing":0.0,
    "created_at":1483682913,
    "updated_at":1483699106,
    "api_count":0,
    "previous_month_api_count":0,
    "include_tags":"",
    "exclude_tags":"",
    "payer_account":false   # this field may take some time to update
}
{% endhighlight %}

------

## Update
Update specified AWS Account Hash

#### Required parameters:

AWS_Account_ID
:  ID of AWS Account which is to be updated

*All params are same as create, required only params those need to modify.

#### Curl Command

{% highlight sh %}
curl -s -XPUT -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/amazon_accounts/<AWS_Account_id>.json -d '{ "aws_role_arn":"<Role ARN>","aws_external_id":"<External ID>","account_number":"<AWS Account Number>","label":"<LABEL>","tags":["<tag1>", "<tag2>"] }'
{% endhighlight %}

#### Curl Response
{% highlight ruby %}
{
    "id":1,
    "account_number":"<Account Number>",
    "access_key_id":"dummy_access_key",
    "secret_access_key":"dummy_secret_key",
    "aws_role_arn":"<Role ARN>",
    "aws_external_id":"<External ID>",
    "label":"<LABEL>",
    "tags":["<tag1>","<tag2>"],
    "discovery_enabled":true,
    "reading_enabled":true,
    "last_watched_at":null,
    "last_cloudtrail_scan_at":null,
    "monitored_ec2_count":0,
    "unmonitored_ec2_count":0,
    "billing":0.0,
    "created_at":1483682913,
    "updated_at":1483699106,
    "api_count":0,
    "previous_month_api_count":0,
    "include_tags":"",
    "exclude_tags":"",
    "payer_account":false
}
{% endhighlight %}

------

## Delete
Delete the specified AWS Account Hash

#### Required parameters:

AWS_Account_ID
: ID of AWS Account which is to be deleted

#### Curl Command

{% highlight sh %}
curl -s -XDELETE -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/amazon_accounts/<AWS_Account_id>.json
{% endhighlight %}

#### Curl Response

{% highlight sh %}
{}
{% endhighlight %}
