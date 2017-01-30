---
layout: default
title: AWS
---

## Overview

This is an API used to get overview of an AWS Account

### Required Parameters:

amazon_account_id
: Id of AWS account which can be retrieved by [Accounts API](accounts.html)

#### CURL Command, and variations:

{% highlight sh %}
curl -su <APIKEY>:U "https://api.copperegg.com/v2/aws/samples/overview.json?amazon_account_id=<AMAZON_ACCOUNT_ID>"

curl -s  "https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/overview.json?amazon_account_id=<AMAZON_ACCOUNT_ID>"

curl -s -XGET -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/overview.json -d '{ "amazon_account_id":<AMAZON_ACCOUNT_ID> }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "billing":{
        "USD":{
            "current":{
                "AmazonCloudWatch":0,
                "AWSLambda":0,
                "AmazonCloudFront":58.62,
                "AWSSupportDeveloper":49,
                "AmazonWorkSpaces":53.3,
                "AmazonSimpleDB":0,
                "AmazonCloudSearch":25.79,
                "AmazonRedshift":109.27,
                "AmazonDynamoDB":0,
                "AmazonRDS":1754.82,
                "AmazonML":0.44,
                "AmazonElastiCache":244.76,
                "AmazonS3":275.49,
                "AmazonRoute53":78.56,
                "AWSDataTransfer":3305.73,
                "awskms":0,
                "AmazonKinesis":13.11,
                "AWSQueueService":155.89,
                "AWSCloudTrail":0,
                "AmazonEC2":14257.85,
                "AmazonSNS":0,
                "AmazonWorkDocs":0
            },
            "monthly":[],
            "currency":"USD","current_month":"2017-01"
        }
    },
    "regions":{
        "us-east-1":{
            "ec2":84,
            "ebs":185,
            "rds":5,
            "dynamo_db":1,
            "elasti_cache":3,
            "redshift":0,
            "sqs":36,
            "swf":0,
            "custommetrics":0,
            "cloudsearch":0,
            "sns":22,
            "elb":36,
            "emr":0,
            "asg":44,
            "s3":37,
            "kinesis":0,
            "route53":1,
            "ml":0,
            "opsworks":1,
            "cloudfront":1,
            "sg":0,
            "workspaces":0,
            "events":21
        },
        "us-west-2":{...},
        "us-west-1":{...},
        "eu-west-1":{...},
        "ap-southeast-1":{...},
        "ap-southeast-2":{...},
        "ap-northeast-1":{...},
        "sa-east-1":{...},
        "eu-central-1":{...}
    },
    "status":{
        "AWS/EC2":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/EBS":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/RDS":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/DynamoDB":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/ElastiCache":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/Redshift":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/SQS":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/SWF":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/CustomMetrics":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/CloudSearch":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/SNS":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/S3":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/ELB":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/ElasticMapReduce":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/AutoScaling":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/Kinesis":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/Route53":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/OpsWorks":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/CloudFront":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/StorageGateway":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/WorkSpaces":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/ML":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/Events":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1]
    },
    "status_logs":{
        "AWS/EC2":[null,null,null,null,null,null,null,null,
                    null,null,null,null,null,null,null,null,null,
                    null,null,null,null,null,null,null,null
                  ],
        "AWS/EBS":[...],
        "AWS/RDS":[...],
        "AWS/DynamoDB":[...],
        "AWS/ElastiCache":[...],
        "AWS/Redshift":[...],
        "AWS/SQS":[...],
        "AWS/SWF":[...],
        "AWS/CustomMetrics":[...],
        "AWS/CloudSearch":[...],
        "AWS/SNS":[...],
        "AWS/S3":[...],
        "AWS/ELB":[...],
        "AWS/ElasticMapReduce":[...],
        "AWS/AutoScaling":[...],
        "AWS/Kinesis":[...],
        "AWS/Route53":[...],
        "AWS/OpsWorks":[...],
        "AWS/CloudFront":[...],
        "AWS/StorageGateway":[...],
        "AWS/WorkSpaces":[...],
        "AWS/ML":[...],
        "AWS/Events":[...]
    },
    "metrics":{
        "AWS/AutoScaling":{"objects":53,"metrics":265},
        "AWS/Billing":{"objects":56,"metrics":56},
        "AWS/CloudFront":{"objects":1,"metrics":6},
        "AWS/DynamoDB":{"objects":1,"metrics":5},
        "AWS/EBS":{"objects":203,"metrics":1624},
        "AWS/EC2":{"objects":95,"metrics":665},
        "AWS/ElastiCache":{"objects":6,"metrics":160},
        "AWS/ELB":{"objects":36,"metrics":180},
        "AWS/Events":{"objects":21,"metrics":63},
        "AWS/OpsWorks":{"objects":1,"metrics":15},
        "AWS/RDS":{"objects":5,"metrics":70},
        "AWS/Route53":{"objects":1,"metrics":2},
        "AWS/S3":{"objects":37,"metrics":74},
        "AWS/SNS":{"objects":22,"metrics":88},
        "AWS/SQS":{"objects":40,"metrics":320}},
        "ec2":{"unmonitored":95,"monitored":0,"reserved":{}
    }
}
{% endhighlight %}

---

## Summary
This is an API used to get summary of an AWS Account

### Required Parameters:

amazon_account_id
: Id of AWS account which can be retrieved by [Accounts API](accounts.html)

#### CURL Command, and variations:

{% highlight sh %}
curl -su <APIKEY>:U "https://api.copperegg.com/v2/aws/samples/summary.json?amazon_account_id=<AMAZON_ACCOUNT_ID>"

curl -s  "https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/summary.json?amazon_account_id=<AMAZON_ACCOUNT_ID>"

curl -s -XGET -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/summary.json -d '{ "amazon_account_id":<AMAZON_ACCOUNT_ID> }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "billing":{
        "USD":{
            "current":{
                "AmazonCloudWatch":0,
                "AWSLambda":0,
                "AmazonCloudFront":58.62,
                "AWSSupportDeveloper":49,
                "AmazonWorkSpaces":53.3,
                "AmazonSimpleDB":0,
                "AmazonCloudSearch":25.79,
                "AmazonRedshift":109.27,
                "AmazonDynamoDB":0,
                "AmazonRDS":1754.82,
                "AmazonML":0.44,
                "AmazonElastiCache":244.76,
                "AmazonS3":275.49,
                "AmazonRoute53":78.56,
                "AWSDataTransfer":3305.73,
                "awskms":0,
                "AmazonKinesis":13.11,
                "AWSQueueService":155.89,
                "AWSCloudTrail":0,
                "AmazonEC2":14257.85,
                "AmazonSNS":0,
                "AmazonWorkDocs":0
            },
            "monthly":[],
            "currency":"USD","current_month":"2017-01"
        }
    },
    "regions":{
        "us-east-1":{
            "ec2":84,
            "ebs":185,
            "rds":5,
            "dynamo_db":1,
            "elasti_cache":3,
            "redshift":0,
            "sqs":36,
            "swf":0,
            "custommetrics":0,
            "cloudsearch":0,
            "sns":22,
            "elb":36,
            "emr":0,
            "asg":44,
            "s3":37,
            "kinesis":0,
            "route53":1,
            "ml":0,
            "opsworks":1,
            "cloudfront":1,
            "sg":0,
            "workspaces":0,
            "events":21
        },
        "us-west-2":{...},
        "us-west-1":{...},
        "eu-west-1":{...},
        "ap-southeast-1":{...},
        "ap-southeast-2":{...},
        "ap-northeast-1":{...},
        "sa-east-1":{...},
        "eu-central-1":{...}
    },
    "status":{
        "AWS/EC2":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/EBS":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/RDS":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/DynamoDB":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/ElastiCache":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/Redshift":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/SQS":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/SWF":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/CustomMetrics":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/CloudSearch":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/SNS":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/S3":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/ELB":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/ElasticMapReduce":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/AutoScaling":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/Kinesis":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/Route53":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/OpsWorks":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/CloudFront":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/StorageGateway":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/WorkSpaces":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/ML":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
        "AWS/Events":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1]
    },
    "status_logs":{
        "AWS/EC2":[null,null,null,null,null,null,null,null,
                    null,null,null,null,null,null,null,null,null,
                    null,null,null,null,null,null,null,null
                  ],
        "AWS/EBS":[...],
        "AWS/RDS":[...],
        "AWS/DynamoDB":[...],
        "AWS/ElastiCache":[...],
        "AWS/Redshift":[...],
        "AWS/SQS":[...],
        "AWS/SWF":[...],
        "AWS/CustomMetrics":[...],
        "AWS/CloudSearch":[...],
        "AWS/SNS":[...],
        "AWS/S3":[...],
        "AWS/ELB":[...],
        "AWS/ElasticMapReduce":[...],
        "AWS/AutoScaling":[...],
        "AWS/Kinesis":[...],
        "AWS/Route53":[...],
        "AWS/OpsWorks":[...],
        "AWS/CloudFront":[...],
        "AWS/StorageGateway":[...],
        "AWS/WorkSpaces":[...],
        "AWS/ML":[...],
        "AWS/Events":[...]
    },
    "metrics":{
        "AWS/AutoScaling":{"objects":53,"metrics":265},
        "AWS/Billing":{"objects":56,"metrics":56},
        "AWS/CloudFront":{"objects":1,"metrics":6},
        "AWS/DynamoDB":{"objects":1,"metrics":5},
        "AWS/EBS":{"objects":203,"metrics":1624},
        "AWS/EC2":{"objects":95,"metrics":665},
        "AWS/ElastiCache":{"objects":6,"metrics":160},
        "AWS/ELB":{"objects":36,"metrics":180},
        "AWS/Events":{"objects":21,"metrics":63},
        "AWS/OpsWorks":{"objects":1,"metrics":15},
        "AWS/RDS":{"objects":5,"metrics":70},
        "AWS/Route53":{"objects":1,"metrics":2},
        "AWS/S3":{"objects":37,"metrics":74},
        "AWS/SNS":{"objects":22,"metrics":88},
        "AWS/SQS":{"objects":40,"metrics":320}},
        "ec2":{"unmonitored":95,"monitored":0,"reserved":{}
    }
}
{% endhighlight %}

---

## Billing
This is an API used to get billing of an AWS Account

### Required Parameters:

amazon_account_id
: Id of AWS account whose billing is to be fetched

date_str
: Date of month for which billing is to be fetched

### Optional Parameters:

overview
: Overview will give billing overview of all AWS accounts


#### CURL Command, and variations:

{% highlight sh %}
curl -su <APIKEY>:U "https://api.copperegg.com/v2/aws/samples/billing.json?amazon_account_id=<AMAZON_ACCOUNT_ID>&date_str=2017-01-01"

curl -s "https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/billing.json?amazon_account_id=<AMAZON_ACCOUNT_ID>&date_str=2017-01-01"

curl -s "https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/billing.json?amazon_account_id=<AMAZON_ACCOUNT_ID>&date_str=2017-01-01&overview=overview"

curl -s -XGET -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/billing.json -d '{ "amazon_account_id":<AMAZON_ACCOUNT_ID>,"date_str":"2017-01-01" }'

curl -s -XGET -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/billing.json -d '{ "amazon_account_id":<AMAZON_ACCOUNT_ID>,"date_str":"2017-01-01","overview":"overview" }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "month_label":"Jan 2017",
    "month_sortable":"2017-01",
    "currencies":{
        "USD":{
            "AmazonSimpleDB":0,
            "AWSLambda":0,
            "AmazonKinesis":13.11,
            "AWSQueueService":155.89,
            "AmazonWorkDocs":0,
            "AmazonML":0.44,
            "AmazonElastiCache":244.76,
            "AWSSupportDeveloper":49,
            "AmazonRDS":1754.82,
            "AmazonSNS":0,
            "AmazonCloudFront":58.62,
            "AWSDataTransfer":3305.73,
            "awskms":0,
            "AmazonRedshift":109.27,
            "AmazonDynamoDB":0,
            "AWSCloudTrail":0,
            "AmazonCloudSearch":25.79,
            "AmazonS3":275.49,
            "AmazonCloudWatch":0,
            "AmazonWorkSpaces":53.3,
            "AmazonRoute53":78.56,
            "AmazonEC2":14257.85
        }
    }
}
{% endhighlight %}

---

## Consolidated billing details

This is an API used to get consolidated billing details of an AWS Account

### Required Parameters:

amazon_account_id
: Id of AWS account whose Consolidated billing is to be fetched

date_str
: Date of month for which consolidated billing is to be fetched

### Optional Parameters:

overview
: Overview will give consolidated billing overview of all AWS accounts


#### CURL Command, and variations:

{% highlight sh %}
curl -su <APIKEY>:U "https://api.copperegg.com/v2/aws/samples/consolidated_billing_details.json?amazon_account_id=<AMAZON_ACCOUNT_ID>&date_str=2017-01-01"

curl -s "https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/consolidated_billing_details.json?amazon_account_id=<AMAZON_ACCOUNT_ID>&date_str=2017-01-01"

curl -s "https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/consolidated_billing_details.json?amazon_account_id=<AMAZON_ACCOUNT_ID>&date_str=2017-01-01&overview=overview"

curl -s -XGET -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/consolidated_billing_details.json -d '{ "amazon_account_id":<AMAZON_ACCOUNT_ID>,"date_str":"2017-01-01" }'

curl -s -XGET -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/consolidated_billing_details.json -d '{ "amazon_account_id":<AMAZON_ACCOUNT_ID>,"date_str":"2017-01-01","overview":"overview" }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "month_label":"Jan 2017",
    "month_sortable":"2017-01",
    "currencies":{
        "USD":{
            "AmazonML":0.44,
            "AmazonS3":275.49,
            "AmazonCloudSearch":25.79,
            "AmazonCloudFront":58.62,
            "AWSSupportDeveloper":49,
            "AmazonCloudWatch":0,
            "AmazonSNS":0,
            "awskms":0,
            "AmazonKinesis":13.11,
            "AWSQueueService":155.89,
            "AmazonRoute53":78.56,
            "AmazonDynamoDB":0,
            "AmazonSimpleDB":0,
            "AWSLambda":0,
            "AmazonRedshift":109.27,
            "AWSCloudTrail":0,
            "AmazonEC2":14257.85,
            "AmazonWorkDocs":0,
            "AWSDataTransfer":3305.73,
            "AmazonRDS":1754.82,
            "AmazonElastiCache":244.76,
            "AmazonWorkSpaces":53.3
        },
        "123456789001":{
            "AmazonSNS":0,
            "AWSCloudTrail":0,
            "AmazonCloudWatch":0,
            "AmazonCloudFront":58.53,
            "AWSSupportDeveloper":49,
            "AmazonS3":273,
            "AmazonDynamoDB":0,
            "AmazonSimpleDB":0,
            "AWSQueueService":155.77,
            "AmazonRDS":1745.68,
            "AmazonRoute53":77.48,
            "AmazonEC2":13848.37,
            "awskms":0,
            "AWSLambda":0,
            "AmazonElastiCache":236.45,
            "AWSDataTransfer":3305.49
        },
        "123456789002":{
            "AmazonRDS":9.14,
            "AmazonML":0.44,
            "AmazonS3":2.48,
            "AmazonElastiCache":8.3,
            "AmazonWorkSpaces":53.3,
            "AWSDataTransfer":0.06,
            "AmazonSNS":0,
            "AmazonRedshift":109.27,
            "AWSCloudTrail":0,
            "AmazonDynamoDB":0,
            "AmazonRoute53":1.08,
            "AWSQueueService":0.12,
            "AmazonSimpleDB":0,
            "AmazonEC2":409.45,
            "AmazonWorkDocs":0,
            "AmazonKinesis":13.11,
            "AmazonCloudSearch":25.79
        }
    }
}
{% endhighlight %}

---

## EC2

This is an API used to get samples of one or more EC2 instances

### EC2 Sample Keys
{% highlight sh %}
Key name           Valid combinations

Cpu                c
Network            n
Status             s
{% endhighlight %}

### Fetch Samples from all AWS Accounts

#### Required Parameters:

overview
: Only existence of key is required

idvs
: It is a list of ids(unique for every ec2 instance)

*idv is a combination of Amazon Account Number \| region \| EC2 instance id\|

eg. 123456789001\|us-east-1\|i-0063cb19c5cce6512\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/ec2.json -d '{ "overview":"overview","idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|i-0016986665842b75b|":{
        "c":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "n":{
            "1484810160":[533795466,30448340], # [rx, tx]
            "1484810220":[null,null],
            "1484810280":[null,null],
            "1484810340":[null,null],
            "1484810400":[null,null],
            "1484810460":[518838963,27407162],
            "1484810520":[null,null],
            "1484810580":[null,null],
            "1484810640":[null,null],
            "1484810700":[null,null],
            "1484810760":[538864838,30779112],
            "1484810820":[null,null],
            "1484810880":[null,null],
            "1484810940":[null,null],
            "1484811000":[null,null],
            "1484811060":[537105814,30708289],
            "1484811120":[null,null],
            "1484811180":[null,null],
            "1484811240":[null,null],
            "1484811300":[null,null],
            "1484811360":[517472163,30531507],
            "1484811420":[null,null],
            "1484811480":[null,null],
            "1484811540":[null,null],
            "1484811600":[null,null]
        },
        "s":{
            "1484810160":[0,0], # [status_check_failed_instance, status_check_failed_system]
            "1484810220":[0,0],
            "1484810280":[0,0],
            "1484810340":[0,0],
            "1484810400":[0,0],
            "1484810460":[0,0],
            "1484810520":[0,0],
            "1484810580":[0,0],
            "1484810640":[0,0],
            "1484810700":[0,0],
            "1484810760":[0,0],
            "1484810820":[0,0],
            "1484810880":[0,0],
            "1484810940":[0,0],
            "1484811000":[0,0],
            "1484811060":[0,0],
            "1484811120":[0,0],
            "1484811180":[0,0],
            "1484811240":[0,0],
            "1484811300":[0,0],
            "1484811360":[0,0],
            "1484811420":[0,0],
            "1484811480":[0,0],
            "1484811540":[0,0],
            "1484811600":[0,0]
        }
    }
}
{% endhighlight %}

### Fetch Samples of specific AWS Account

#### Required Parameters:

amazon_account_id
: ID of an AWS account to which EC2 instance belongs

idvs
: It is a list of ids(unique for every ec2 instance)

*idv is a combination of region \| EC2 instance id\|

eg. us-east-1\|i-0063cb19c5cce6512\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/ec2.json -d '{ "amazon_account_id":<Amazon Account ID>,"idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|i-0016986665842b75b|":{
        "c":{
            "1484810160":0.341,
            "1484810460":0.328,
            "1484810760":0.364,
            "1484811060":0.348,
            "1484811360":0.329
        },
        "n":{
            "1484810160":[533795466,30448340],
            "1484810220":[null,null],
            "1484810280":[null,null],
            "1484810340":[null,null],
            "1484810400":[null,null],
            "1484810460":[518838963,27407162],
            "1484810520":[null,null],
            "1484810580":[null,null],
            "1484810640":[null,null],
            "1484810700":[null,null],
            "1484810760":[538864838,30779112],
            "1484810820":[null,null],
            "1484810880":[null,null],
            "1484810940":[null,null],
            "1484811000":[null,null],
            "1484811060":[537105814,30708289],
            "1484811120":[null,null],
            "1484811180":[null,null],
            "1484811240":[null,null],
            "1484811300":[null,null],
            "1484811360":[517472163,30531507],
            "1484811420":[null,null],
            "1484811480":[null,null],
            "1484811540":[null,null],
            "1484811600":[null,null]
        },
        "s":{
            "1484810160":[0,0],
            "1484810220":[0,0],
            "1484810280":[0,0],
            "1484810340":[0,0],
            "1484810400":[0,0],
            "1484810460":[0,0],
            "1484810520":[0,0],
            "1484810580":[0,0],
            "1484810640":[0,0],
            "1484810700":[0,0],
            "1484810760":[0,0],
            "1484810820":[0,0],
            "1484810880":[0,0],
            "1484810940":[0,0],
            "1484811000":[0,0],
            "1484811060":[0,0],
            "1484811120":[0,0],
            "1484811180":[0,0],
            "1484811240":[0,0],
            "1484811300":[0,0],
            "1484811360":[0,0],
            "1484811420":[0,0],
            "1484811480":[0,0],
            "1484811540":[0,0],
            "1484811600":[0,0]
        }
    }
}
{% endhighlight %}

---

## EBS

This is an API used to get samples of one or more EBS Volumes

### EBS Sample Keys
{% highlight sh %}
Key name                         Valid combinations

Volume(bytes)                    b
Volume operations                o
Total volume                     t
Queue length                     q
Volume tp                        p
Cons. operations                 c
{% endhighlight %}

### Fetch Samples from all AWS Accounts

#### Required Parameters:

overview
: Only existence of key is required

idvs
: It is a list of ids(unique for every ebs volume)

*idv is a combination of Amazon Account Number \| region \| EBS volume id \|

eg. 123456789001\|us-east-1\|vol-0063cb19c5cce6512\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/ebs.json -d '{ "overview":"overview","idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|vol-00018cad1c7bc0195|":{
        "b":{
            "1484812200":[4096,8158],  # [read,write]
            "1484812800":[20055,8398],
            "1484813400":[4096,8328]
        },
        "o":{
            "1484812200":[5,121],      # [read,write]
            "1484812800":[463,139],
            "1484813400":[5,120]
        },
        "t":{
            "1484812200":[0.002,8.0e-05,299.98], # [read,write,idle]
            "1484812800":[0.00108,0.00129,299.83],
            "1484813400":[0.0,0.00067,299.92]
        },
        "q":{
            "1484812200":0,
            "1484812800":0,
            "1484813400":0
        },
        "p":{},
        "c":{}
    }
}
{% endhighlight %}

### Fetch Samples of specific AWS Account

#### Required Parameters:

amazon_account_id
: ID of an AWS account to which EBS Volume belongs

idvs
: It is a list of ids(unique for every ebs volume)

*idv is a combination of region \| EBS volume id \|

eg. us-east-1\|vol-0063cb19c5cce6512\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/ebs.json -d '{ "amazon_account_id":<Amazon Account ID>,"idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|vol-00018cad1c7bc0195|":{
        "b":{
            "1484812200":[4096,8158],
            "1484812800":[20055,8398],
            "1484813400":[4096,8328]
        },
        "o":{
            "1484812200":[5,121],
            "1484812800":[463,139],
            "1484813400":[5,120]
        },
        "t":{
            "1484812200":[0.002,8.0e-05,299.98],
            "1484812800":[0.00108,0.00129,299.83],
            "1484813400":[0.0,0.00067,299.92]
        },
        "q":{
            "1484812200":0,
            "1484812800":0,
            "1484813400":0
        },
        "p":{},
        "c":{}
    }
}
{% endhighlight %}

---

## DynamoDB

This is an API used to get samples of one or more dynamodb tables

### Dynamodb Sample Keys
{% highlight sh %}
Key name                         Valid combinations

Data                             d
{% endhighlight %}

### Fetch Samples from all AWS Accounts

#### Required Parameters:

overview
: Only existence of key is required

idvs
: It is a list of ids(unique for every dynamodb)

*idv is a combination of Amazon Account Number \| region \| dynamodb name \|

eg. 123456789001\|us-east-1\|demo-table\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/dynamodb.json -d '{ "overview":"overview","idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|demo-table|":{
        "d":{
            "1484896500":[null,null,null,null,13,8,null,null,null,null,null,null], # [latencty, user_error, system_error, thr_requests, prov_read, prov_write, cons_read, cons_write, returned, conditional_check_failed_requests, online_index_throttle_events, online_index_consumed_write_capacity]
            "1484896800":[null,null,null,null,13,8,null,null,null,null,null,null],
            "1484897100":[null,null,null,null,13,8,null,null,null,null,null,null],
            "1484897400":[null,null,null,null,13,8,null,null,null,null,null,null],
            "1484897700":[null,null,null,null,13,8,null,null,null,null,null,null],
            "1484898000":[null,null,null,null,13,8,null,null,null,null,null,null],
            "1484898300":[null,null,null,null,13,8,null,null,null,null,null,null],
            "1484898600":[null,null,null,null,13,8,null,null,null,null,null,null],
            "1484898900":[null,null,null,null,13,8,null,null,null,null,null,null],
            "1484899200":[null,null,null,null,13,8,null,null,null,null,null,null],
            "1484899500":[null,null,null,null,13,8,null,null,null,null,null,null]
        }
    }
}
{% endhighlight %}

### Fetch Samples of specific AWS Account

#### Required Parameters:

amazon_account_id
: ID of an AWS account to which dynamodb belongs

idvs
: It is a list of ids(unique for every dynamodb)

*idv is a combination of region \| dynamodb name \|

eg. us-east-1\|demo-table\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/dynamodb.json -d '{ "amazon_account_id":<Amazon Account ID>,"idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|demo-table|":{
        "d":{
            "1484896500":[null,null,null,null,13,8,null,null,null,null,null,null],
            "1484896800":[null,null,null,null,13,8,null,null,null,null,null,null],
            "1484897100":[null,null,null,null,13,8,null,null,null,null,null,null],
            "1484897400":[null,null,null,null,13,8,null,null,null,null,null,null],
            "1484897700":[null,null,null,null,13,8,null,null,null,null,null,null],
            "1484898000":[null,null,null,null,13,8,null,null,null,null,null,null],
            "1484898300":[null,null,null,null,13,8,null,null,null,null,null,null],
            "1484898600":[null,null,null,null,13,8,null,null,null,null,null,null],
            "1484898900":[null,null,null,null,13,8,null,null,null,null,null,null],
            "1484899200":[null,null,null,null,13,8,null,null,null,null,null,null],
            "1484899500":[null,null,null,null,13,8,null,null,null,null,null,null]
        }
    }
}
{% endhighlight %}

---

## RDS

This is an API used to get samples of one or more RDS instances

### RDS Sample Keys
{% highlight sh %}
Key name                         Valid combinations

Data                             r
Latency                          l
Cpu                              c
{% endhighlight %}

### Fetch Samples from all AWS Accounts

#### Required Parameters:

overview
: Only existence of key is required

idvs
: It is a list of ids(unique for every RDS)

*idv is a combination of Amazon Account Number \| region \| RDS instance name \|

eg. 123456789001\|us-east-1\|rds-test-1\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/rds.json -d '{ "overview":"overview","idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|rds-test-1|":{
        "c":{
            "1484898840":0.013,
            "1484898900":0.018,
            "1484898960":0.015,
            "1484899020":0.012,
            "1484899080":0.015,
            "1484899140":0.016,
            "1484899200":0.022,
            "1484899260":0.014,
            "1484899320":0.013,
            "1484899380":0.013,
            "1484899440":0.015,
            "1484899500":0.015,
            "1484899560":0.017,
            "1484899620":0.013,
            "1484899680":0.013,
            "1484899740":0.017,
            "1484899800":0.019,
            "1484899860":0.011,
            "1484899920":0.016,
            "1484899980":0.013,
            "1484900040":0.012,
            "1484900100":0.022,
            "1484900160":0.015,
            "1484900220":0.014
        },
        "l":{
            "1484898840":[0.0,0.005], # [read, write]
            "1484898900":[0.0,0.005],
            "1484898960":[0.0,0.006],
            "1484899020":[0.0,0.008],
            "1484899080":[0.0,0.005],
            "1484899140":[0.0,0.01],
            "1484899200":[0.0,0.008],
            "1484899260":[0.0,0.007],
            "1484899320":[0.0,0.005],
            "1484899380":[0.0,0.006],
            "1484899440":[0.0,0.004],
            "1484899500":[0.001,0.004],
            "1484899560":[0.0,0.006],
            "1484899620":[0.0,0.007],
            "1484899680":[0.0,0.005],
            "1484899740":[0.0,0.011],
            "1484899800":[0.002,0.006],
            "1484899860":[0.0,0.006],
            "1484899920":[0.0,0.004],
            "1484899980":[0.0,0.005],
            "1484900040":[0.0,0.005],
            "1484900100":[0.0,0.005],
            "1484900160":[0.0,0.012],
            "1484900220":[0.0,0.007],
            "1484900280":[0.0,0.005]
        },
        "r":{
            "1484898840":[7364288512,0,1,0,14950,615,17932], # [freeable_memory, read_iops, write_iops, read_throughput, write_throughput, network_receive_throughput, network_transmit_throughput]
            "1484898900":[7363944448,1,2,682,29764,900,33123],
            "1484898960":[7364173824,0,2,0,39525,1216,44446],
            "1484899020":[7363866624,0,4,0,77344,1530,81533],
            "1484899080":[7363923968,0,1,0,21367,622,24427],
            "1484899140":[7364030464,0,9,0,159473,2760,165361],
            "1484899200":[7364128768,1,2,750,29900,1060,34686],
            "1484899260":[7363678208,0,3,0,54135,1164,57913],
            "1484899320":[7364431872,0,3,0,47235,1229,50994],
            "1484899380":[7364440064,0,5,0,83771,1740,88296],
            "1484899440":[7364743168,0,1,0,12629,613,15484],
            "1484899500":[7364345856,1,2,682,25053,846,28420],
            "1484899560":[7364501504,0,3,0,51746,1302,56185],
            "1484899620":[7364653056,0,4,0,71270,1540,75490],
            "1484899680":[7364964352,0,1,0,16247,526,19243],
            "1484899740":[7364599808,0,7,0,122743,2250,128104],
            "1484899800":[7364632576,1,4,682,68947,1501,74131],
            "1484899860":[7364841472,0,3,0,46628,1057,50445],
            "1484899920":[7364767744,0,2,0,28944,763,32040],
            "1484899980":[7364636672,0,4,0,70295,1425,74245],
            "1484900040":[7364530176,0,1,0,12632,629,15647],
            "1484900100":[7364427776,1,2,682,28056,916,31510],
            "1484900160":[7364112384,0,7,0,115715,2415,121579],
            "1484900220":[7364222976,0,6,0,98915,2019,103907],
            "1484900280":[7364284416,0,1,0,21846,640,24980]
        }
    }
}
{% endhighlight %}

### Fetch Samples of specific AWS Account

#### Required Parameters:

amazon_account_id
: ID of an AWS account to which rds belongs

idvs
: It is a list of ids(unique for every rds)

*idv is a combination of region \| rds instance name \|

eg. us-east-1\|demo-table\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/rds.json -d '{ "amazon_account_id":<Amazon Account ID>,"idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|rds-test-1|":{
        "c":{
            "1484898840":0.013,
            "1484898900":0.018,
            "1484898960":0.015,
            "1484899020":0.012,
            "1484899080":0.015,
            "1484899140":0.016,
            "1484899200":0.022,
            "1484899260":0.014,
            "1484899320":0.013,
            "1484899380":0.013,
            "1484899440":0.015,
            "1484899500":0.015,
            "1484899560":0.017,
            "1484899620":0.013,
            "1484899680":0.013,
            "1484899740":0.017,
            "1484899800":0.019,
            "1484899860":0.011,
            "1484899920":0.016,
            "1484899980":0.013,
            "1484900040":0.012,
            "1484900100":0.022,
            "1484900160":0.015,
            "1484900220":0.014
        },
        "l":{
            "1484898840":[0.0,0.005],
            "1484898900":[0.0,0.005],
            "1484898960":[0.0,0.006],
            "1484899020":[0.0,0.008],
            "1484899080":[0.0,0.005],
            "1484899140":[0.0,0.01],
            "1484899200":[0.0,0.008],
            "1484899260":[0.0,0.007],
            "1484899320":[0.0,0.005],
            "1484899380":[0.0,0.006],
            "1484899440":[0.0,0.004],
            "1484899500":[0.001,0.004],
            "1484899560":[0.0,0.006],
            "1484899620":[0.0,0.007],
            "1484899680":[0.0,0.005],
            "1484899740":[0.0,0.011],
            "1484899800":[0.002,0.006],
            "1484899860":[0.0,0.006],
            "1484899920":[0.0,0.004],
            "1484899980":[0.0,0.005],
            "1484900040":[0.0,0.005],
            "1484900100":[0.0,0.005],
            "1484900160":[0.0,0.012],
            "1484900220":[0.0,0.007],
            "1484900280":[0.0,0.005]
        },
        "r":{
            "1484898840":[7364288512,0,1,0,14950,615,17932],
            "1484898900":[7363944448,1,2,682,29764,900,33123],
            "1484898960":[7364173824,0,2,0,39525,1216,44446],
            "1484899020":[7363866624,0,4,0,77344,1530,81533],
            "1484899080":[7363923968,0,1,0,21367,622,24427],
            "1484899140":[7364030464,0,9,0,159473,2760,165361],
            "1484899200":[7364128768,1,2,750,29900,1060,34686],
            "1484899260":[7363678208,0,3,0,54135,1164,57913],
            "1484899320":[7364431872,0,3,0,47235,1229,50994],
            "1484899380":[7364440064,0,5,0,83771,1740,88296],
            "1484899440":[7364743168,0,1,0,12629,613,15484],
            "1484899500":[7364345856,1,2,682,25053,846,28420],
            "1484899560":[7364501504,0,3,0,51746,1302,56185],
            "1484899620":[7364653056,0,4,0,71270,1540,75490],
            "1484899680":[7364964352,0,1,0,16247,526,19243],
            "1484899740":[7364599808,0,7,0,122743,2250,128104],
            "1484899800":[7364632576,1,4,682,68947,1501,74131],
            "1484899860":[7364841472,0,3,0,46628,1057,50445],
            "1484899920":[7364767744,0,2,0,28944,763,32040],
            "1484899980":[7364636672,0,4,0,70295,1425,74245],
            "1484900040":[7364530176,0,1,0,12632,629,15647],
            "1484900100":[7364427776,1,2,682,28056,916,31510],
            "1484900160":[7364112384,0,7,0,115715,2415,121579],
            "1484900220":[7364222976,0,6,0,98915,2019,103907],
            "1484900280":[7364284416,0,1,0,21846,640,24980]
        }
    }
}
{% endhighlight %}

---

## ELB

This is an API used to get samples of one or more ELB

### ELB Sample Keys
{% highlight sh %}
Key name                         Valid combinations

Health                           h
Host count                       r
Backend connection               b
Latency                          l
Spill over                       s
{% endhighlight %}

### Fetch Samples from all AWS Accounts

#### Required Parameters:

overview
: Only existence of key is required

idvs
: It is a list of ids(unique for every elb)

*idv is a combination of Amazon Account Number \| region \| elb name \|

eg. 123456789001\|us-east-1\|test-elb\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/elb.json -d '{ "overview":"overview","idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|test-elb|us-east-1a|":{
        "h":{
            "1484844360":[4,0], # [healthy_host_count, unHealthy_Host_Count]
            "1484844420":[4,0],
            "1484844480":[4,0],
            "1484844540":[4,0],
            "1484844600":[4,0],
            "1484844660":[4,0],
            "1484844720":[4,0],
            "1484844780":[4,0],
            "1484844840":[4,0],
            "1484844900":[4,0],
            "1484844960":[4,0],
            "1484845020":[4,0],
            "1484845080":[4,0],
            "1484845140":[4,0],
            "1484845200":[4,0],
            "1484845260":[4,0],
            "1484845320":[4,0],
            "1484845380":[4,0],
            "1484845440":[4,0],
            "1484845500":[4,0],
            "1484845560":[4,0],
            "1484845620":[4,0],
            "1484845680":[4,0],
            "1484845740":[4,0],
            "1484845800":[4,0],
            "1484845860":[4,0],
            "1484845920":[4,0],
            "1484845980":[4,0]
        },
        "r":{
            "1484844360":[15524,1,27], # [request_count, HTTP_code_ELB_5XX, HTTP_code_backend_5XX]
            "1484844420":[14569,null,21],
            "1484844480":[16429,null,20],
            "1484844540":[15969,null,23],
            "1484844600":[14270,null,21],
            "1484844660":[15146,null,19],
            "1484844720":[15694,20,22],
            "1484844780":[16189,null,17],
            "1484844840":[15088,2,18],
            "1484844900":[15064,null,22],
            "1484844960":[16399,null,16],
            "1484845020":[16037,null,20],
            "1484845080":[14059,null,61],
            "1484845140":[14216,null,24],
            "1484845200":[14174,null,23],
            "1484845260":[14547,null,20],
            "1484845320":[15963,null,16],
            "1484845380":[15281,null,24],
            "1484845440":[16173,4,23],
            "1484845500":[15363,null,21],
            "1484845560":[15661,null,24],
            "1484845620":[15402,null,23],
            "1484845680":[14134,null,14],
            "1484845740":[14129,null,27],
            "1484845800":[15116,null,24],
            "1484845860":[14866,null,16],
            "1484845920":[15430,null,137],
            "1484845980":[15626,null,19]
        },
        "b":{},
        "l":{
            "1484844360":0,
            "1484844420":0,
            "1484844480":0,
            "1484844540":0,
            "1484844600":0,
            "1484844660":0,
            "1484844720":0,
            "1484844780":0,
            "1484844840":0,
            "1484844900":0,
            "1484844960":0,
            "1484845020":0,
            "1484845080":0,
            "1484845140":0,
            "1484845200":0,
            "1484845260":0,
            "1484845320":0,
            "1484845380":0,
            "1484845440":0,
            "1484845500":0,
            "1484845560":0,
            "1484845620":0,
            "1484845680":0,
            "1484845740":0,
            "1484845800":0,
            "1484845860":0,
            "1484845920":0,
            "1484845980":0
        },
        "s":{}
    },
    "123456789001|us-east-1|test-elb|us-east-1e|":{
        "h":{...},
        "r":{...},
        "b":{},
        "l":{...},
        "s":{}
    }
}
{% endhighlight %}

### Fetch Samples of specific AWS Account

#### Required Parameters:

amazon_account_id
: ID of an AWS account to which elb belongs

idvs
: It is a list of ids(unique for every elb)

*idv is a combination of region \| elb name \|

eg. us-east-1\|test-elb\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/elb.json -d '{ "amazon_account_id":<Amazon Account ID>,"idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|test-elb|us-east-1a|":{
        "h":{
            "1484844360":[4,0],
            "1484844420":[4,0],
            "1484844480":[4,0],
            "1484844540":[4,0],
            "1484844600":[4,0],
            "1484844660":[4,0],
            "1484844720":[4,0],
            "1484844780":[4,0],
            "1484844840":[4,0],
            "1484844900":[4,0],
            "1484844960":[4,0],
            "1484845020":[4,0],
            "1484845080":[4,0],
            "1484845140":[4,0],
            "1484845200":[4,0],
            "1484845260":[4,0],
            "1484845320":[4,0],
            "1484845380":[4,0],
            "1484845440":[4,0],
            "1484845500":[4,0],
            "1484845560":[4,0],
            "1484845620":[4,0],
            "1484845680":[4,0],
            "1484845740":[4,0],
            "1484845800":[4,0],
            "1484845860":[4,0],
            "1484845920":[4,0],
            "1484845980":[4,0]
        },
        "r":{
            "1484844360":[15524,1,27],
            "1484844420":[14569,null,21],
            "1484844480":[16429,null,20],
            "1484844540":[15969,null,23],
            "1484844600":[14270,null,21],
            "1484844660":[15146,null,19],
            "1484844720":[15694,20,22],
            "1484844780":[16189,null,17],
            "1484844840":[15088,2,18],
            "1484844900":[15064,null,22],
            "1484844960":[16399,null,16],
            "1484845020":[16037,null,20],
            "1484845080":[14059,null,61],
            "1484845140":[14216,null,24],
            "1484845200":[14174,null,23],
            "1484845260":[14547,null,20],
            "1484845320":[15963,null,16],
            "1484845380":[15281,null,24],
            "1484845440":[16173,4,23],
            "1484845500":[15363,null,21],
            "1484845560":[15661,null,24],
            "1484845620":[15402,null,23],
            "1484845680":[14134,null,14],
            "1484845740":[14129,null,27],
            "1484845800":[15116,null,24],
            "1484845860":[14866,null,16],
            "1484845920":[15430,null,137],
            "1484845980":[15626,null,19]
        },
        "b":{},
        "l":{
            "1484844360":0,
            "1484844420":0,
            "1484844480":0,
            "1484844540":0,
            "1484844600":0,
            "1484844660":0,
            "1484844720":0,
            "1484844780":0,
            "1484844840":0,
            "1484844900":0,
            "1484844960":0,
            "1484845020":0,
            "1484845080":0,
            "1484845140":0,
            "1484845200":0,
            "1484845260":0,
            "1484845320":0,
            "1484845380":0,
            "1484845440":0,
            "1484845500":0,
            "1484845560":0,
            "1484845620":0,
            "1484845680":0,
            "1484845740":0,
            "1484845800":0,
            "1484845860":0,
            "1484845920":0,
            "1484845980":0
        },
        "s":{}
    },
    "123456789001|us-east-1|test-elb|us-east-1e|":{
        "h":{...},
        "r":{...},
        "b":{},
        "l":{...},
        "s":{}
    }
}
{% endhighlight %}

---

## Cloudfront

This is an API used to get samples of one or more Cloudfront distributions

### Cloudfront distribution Sample Keys
{% highlight sh %}
Key name                         Valid combinations

4xx                              c
5xx                              p
Total error rate                 t
Bytes uploaded                   u
Bytes downloaded                 d
Requests                         r
{% endhighlight %}

### Fetch Samples from all AWS Accounts

#### Required Parameters:

overview
: Only existence of key is required

idvs
: It is a list of ids(unique for every distribution)

*idv is a combination of Amazon Account Number \| region \| cloudfront distribution id \|

eg. 123456789001\|us-east-1\|E2CN093FFQP6MI\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/cloudfront.json -d '{ "overview":"overview","idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|E2CN093FFQP6MI|Global|":{
        "r":{
            "1484899320":477,
            "1484899380":462,
            "1484899440":456,
            "1484899500":461,
            "1484899560":442,
            "1484899620":428,
            "1484899680":447,
            "1484899740":451,
            "1484899800":488,
            "1484899860":452,
            "1484899920":462,
            "1484899980":306,
            "1484900040":472,
            "1484900100":417,
            "1484900160":455,
            "1484900220":450,
            "1484900280":467,
            "1484900340":448,
            "1484900400":455,
            "1484900460":458,
            "1484900520":464,
            "1484900580":467,
            "1484900640":446,
            "1484900700":441,
            "1484900760":465,
            "1484900820":476,
            "1484900880":170
        },
        "d":{
            "1484899320":1040224,
            "1484899380":1021658,
            "1484899440":1082236,
            "1484899500":1017429,
            "1484899560":976599,
            "1484899620":978355,
            "1484899680":1025726,
            "1484899740":1023372,
            "1484899800":3550806,
            "1484899860":978029,
            "1484899920":1057661,
            "1484899980":688956,
            "1484900040":1017690,
            "1484900100":876026,
            "1484900160":1045381,
            "1484900220":1020924,
            "1484900280":1015863,
            "1484900340":1008790,
            "1484900400":1022612,
            "1484900460":3427201,
            "1484900520":1033952,
            "1484900580":3477979,
            "1484900640":3451604,
            "1484900700":1010439,
            "1484900760":1037872,
            "1484900820":1028954,
            "1484900880":377466
        },
        "u":{
            "1484899320":0,
            "1484899380":0,
            "1484899440":0,
            "1484899500":0,
            "1484899560":0,
            "1484899620":0,
            "1484899680":0,
            "1484899740":0,
            "1484899800":0,
            "1484899860":0,
            "1484899920":0,
            "1484899980":0,
            "1484900040":0,
            "1484900100":0,
            "1484900160":0,
            "1484900220":0,
            "1484900280":0,
            "1484900340":0,
            "1484900400":0,
            "1484900460":0,
            "1484900520":0,
            "1484900580":0,
            "1484900640":0,
            "1484900700":0,
            "1484900760":0,
            "1484900820":0,
            "1484900880":0
        },
        "t":{
            "1484899320":0,
            "1484899380":0,
            "1484899440":0,
            "1484899500":0,
            "1484899560":0,
            "1484899620":0,
            "1484899680":0,
            "1484899740":0,
            "1484899800":0,
            "1484899860":0,
            "1484899920":0,
            "1484899980":0,
            "1484900040":0,
            "1484900100":0,
            "1484900160":0,
            "1484900220":0,
            "1484900280":0,
            "1484900340":0,
            1484900400":0,
            "1484900460":0,
            "1484900520":0,
            "1484900580":0,
            "1484900640":0,
            "1484900700":0,
            "1484900760":0,
            "1484900820":0,
            "1484900880":0
        },
        "p":{
            "1484899320":0,
            "1484899380":0,
            "1484899440":0,
            "1484899500":0,
            "1484899560":0,
            "1484899620":0,
            "1484899680":0,
            "1484899740":0,
            "1484899800":0,
            "1484899860":0,
            "1484899920":0,
            "1484899980":0,
            "1484900040":0,
            "1484900100":0,
            "1484900160":0,
            "1484900220":0,
            "1484900280":0,
            "1484900340":0,
            "1484900400":0,
            "1484900460":0,
            "1484900520":0,
            "1484900580":0,
            "1484900640":0,
            "1484900700":0,
            "1484900760":0,
            "1484900820":0,
            "1484900880":0
        },
        "c":{
            "1484899320":0,
            "1484899380":0,
            "1484899440":0,
            "1484899500":0,
            "1484899560":0,
            "1484899620":0,
            "1484899680":0,
            "1484899740":0,
            "1484899800":0,
            "1484899860":0,
            "1484899920":0,
            "1484899980":0,
            "1484900040":0,
            "1484900100":0,
            "1484900160":0,
            "1484900220":0,
            "1484900280":0,
            "1484900340":0,
            "1484900400":0,
            "1484900460":0,
            "1484900520":0,
            "1484900580":0,
            "1484900640":0,
            "1484900700":0,
            "1484900760":0,
            "1484900820":0,
            "1484900880":0
        }
    }
}
{% endhighlight %}

### Fetch Samples of specific AWS Account

#### Required Parameters:

amazon_account_id
: ID of an AWS account to which cloudfront distribution belongs

idvs
: It is a list of ids(unique for every cloudfront distribution)

*idv is a combination of region \| cloudfront distribution \|

eg. us-east-1\|E2CN093FFQP6MI\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/cloudfront.json -d '{ "amazon_account_id":<Amazon Account ID>,"idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|E2CN093FFQP6MI|Global|":{
        "r":{
            "1484899320":477,
            "1484899380":462,
            "1484899440":456,
            "1484899500":461,
            "1484899560":442,
            "1484899620":428,
            "1484899680":447,
            "1484899740":451,
            "1484899800":488,
            "1484899860":452,
            "1484899920":462,
            "1484899980":306,
            "1484900040":472,
            "1484900100":417,
            "1484900160":455,
            "1484900220":450,
            "1484900280":467,
            "1484900340":448,
            "1484900400":455,
            "1484900460":458,
            "1484900520":464,
            "1484900580":467,
            "1484900640":446,
            "1484900700":441,
            "1484900760":465,
            "1484900820":476,
            "1484900880":170
        },
        "d":{
            "1484899320":1040224,
            "1484899380":1021658,
            "1484899440":1082236,
            "1484899500":1017429,
            "1484899560":976599,
            "1484899620":978355,
            "1484899680":1025726,
            "1484899740":1023372,
            "1484899800":3550806,
            "1484899860":978029,
            "1484899920":1057661,
            "1484899980":688956,
            "1484900040":1017690,
            "1484900100":876026,
            "1484900160":1045381,
            "1484900220":1020924,
            "1484900280":1015863,
            "1484900340":1008790,
            "1484900400":1022612,
            "1484900460":3427201,
            "1484900520":1033952,
            "1484900580":3477979,
            "1484900640":3451604,
            "1484900700":1010439,
            "1484900760":1037872,
            "1484900820":1028954,
            "1484900880":377466
        },
        "u":{
            "1484899320":0,
            "1484899380":0,
            "1484899440":0,
            "1484899500":0,
            "1484899560":0,
            "1484899620":0,
            "1484899680":0,
            "1484899740":0,
            "1484899800":0,
            "1484899860":0,
            "1484899920":0,
            "1484899980":0,
            "1484900040":0,
            "1484900100":0,
            "1484900160":0,
            "1484900220":0,
            "1484900280":0,
            "1484900340":0,
            "1484900400":0,
            "1484900460":0,
            "1484900520":0,
            "1484900580":0,
            "1484900640":0,
            "1484900700":0,
            "1484900760":0,
            "1484900820":0,
            "1484900880":0
        },
        "t":{
            "1484899320":0,
            "1484899380":0,
            "1484899440":0,
            "1484899500":0,
            "1484899560":0,
            "1484899620":0,
            "1484899680":0,
            "1484899740":0,
            "1484899800":0,
            "1484899860":0,
            "1484899920":0,
            "1484899980":0,
            "1484900040":0,
            "1484900100":0,
            "1484900160":0,
            "1484900220":0,
            "1484900280":0,
            "1484900340":0,
            1484900400":0,
            "1484900460":0,
            "1484900520":0,
            "1484900580":0,
            "1484900640":0,
            "1484900700":0,
            "1484900760":0,
            "1484900820":0,
            "1484900880":0
        },
        "p":{
            "1484899320":0,
            "1484899380":0,
            "1484899440":0,
            "1484899500":0,
            "1484899560":0,
            "1484899620":0,
            "1484899680":0,
            "1484899740":0,
            "1484899800":0,
            "1484899860":0,
            "1484899920":0,
            "1484899980":0,
            "1484900040":0,
            "1484900100":0,
            "1484900160":0,
            "1484900220":0,
            "1484900280":0,
            "1484900340":0,
            "1484900400":0,
            "1484900460":0,
            "1484900520":0,
            "1484900580":0,
            "1484900640":0,
            "1484900700":0,
            "1484900760":0,
            "1484900820":0,
            "1484900880":0
        },
        "c":{
            "1484899320":0,
            "1484899380":0,
            "1484899440":0,
            "1484899500":0,
            "1484899560":0,
            "1484899620":0,
            "1484899680":0,
            "1484899740":0,
            "1484899800":0,
            "1484899860":0,
            "1484899920":0,
            "1484899980":0,
            "1484900040":0,
            "1484900100":0,
            "1484900160":0,
            "1484900220":0,
            "1484900280":0,
            "1484900340":0,
            "1484900400":0,
            "1484900460":0,
            "1484900520":0,
            "1484900580":0,
            "1484900640":0,
            "1484900700":0,
            "1484900760":0,
            "1484900820":0,
            "1484900880":0
        }
    }
}
{% endhighlight %}

---

## Opsworks

This is an API used to get samples of one or more opsworks stacks

### Opsworks stack Sample Keys
{% highlight sh %}
Key name                         Valid combinations

Memory                           m
Load                             l
Cpu                              c
{% endhighlight %}

### Fetch Samples from all AWS Accounts

#### Required Parameters:

overview
: Only existence of key is required

idvs
: It is a list of ids(unique for every opsworks stack)

*idv is a combination of Amazon Account Number \| region \| opsworks stack id \|

eg. 123456789001\|us-east-1\|2a28e197-3e6c-4ebc-99b7-e183d47ad627\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/opsworks.json -d '{ "overview":"overview","idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "601337641757|us-east-1|ffd7f8f4-1d34-47ed-96b3-ea0ad505ffef|":{
        "c":{
            "1484899440":0.9997,
            "1484899500":0.9997,
            "1484899560":0.9997,
            "1484899620":0.9963,
            "1484899680":0.9997,
            "1484899740":0.9997,
            "1484899800":0.9997,
            "1484899860":0.9997,
            "1484899920":0.9997,
            "1484899980":0.9997,
            "1484900040":0.9997,
            "1484900100":0.998,
            "1484900160":0.9997,
            "1484900220":0.9997,
            "1484900280":0.9997,
            "1484900340":0.9997,
            "1484900400":0.998,
            "1484900460":0.9997,
            "1484900520":0.9997,
            "1484900580":0.9963,
            "1484900640":0.9947,
            "1484900700":0.9963,
            "1484900760":0.9963,
            "1484900820":0.9997,
            "1484900880":0.9997,
            "1484900940":0.9997,
            "1484901000":0.9997,
            "1484901060":0.9997,
            "1484901120":0.9997
        },
        "l":{
            "1484899440":0.0,
            "1484899500":0.0,
            "1484899560":0.0,
            "1484899620":0.0,
            "1484899680":0.0,
            "1484899740":0.0,
            "1484899800":0.0,
            "1484899860":0.0,
            "1484899920":0.0,
            "1484899980":0.0,
            "1484900040":0.0,
            "1484900100":0.0,
            "1484900160":0.0,
            "1484900220":0.0,
            "1484900280":0.0,
            "1484900340":0.0,
            "1484900400":0.0,
            "1484900460":0.0,
            "1484900520":0.0,
            "1484900580":0.0,
            "1484900640":0.0,
            "1484900700":0.0,
            "1484900760":0.0,
            "1484900820":0.0,
            "1484900880":0.0,
            "1484900940":0.0,
            "1484901000":0.0,
            "1484901060":0.0,
            "1484901120":0.0
        },
        "m":{
            "1484899440":[2852872.0,449784.0], # [free, used]
            "1484899500":[2852932.0,449724.0],
            "1484899560":[2852248.0,450388.0],
            "1484899620":[2850172.0,452464.0],
            "1484899680":[2851228.0,451404.0],
            "1484899740":[2851504.0,451124.0],
            "1484899800":[2851380.0,451236.0],
            "1484899860":[2851260.0,451348.0],
            "1484899920":[2851384.0,451220.0],
            "1484899980":[2851944.0,450652.0],
            "1484900040":[2852484.0,450108.0],
            "1484900100":[2852748.0,449836.0],
            "1484900160":[2851564.0,451008.0],
            "1484900220":[2851380.0,451188.0],
            "1484900280":[2851632.0,450932.0],
            "1484900340":[2851940.0,450620.0],
            "1484900400":[2851444.0,451108.0],
            "1484900460":[2851816.0,450724.0],
            "1484900520":[2851324.0,451212.0],
            "1484900580":[2850932.0,451592.0],
            "1484900640":[2850452.0,452020.0],
            "1484900700":[2850620.0,451800.0],
            "1484900760":[2850144.0,452212.0],
            "1484900820":[2851816.0,450524.0],
            "1484900880":[2852684.0,449656.0],
            "1484900940":[2852684.0,449656.0],
            "1484901000":[2852680.0,449660.0],
            "1484901060":[2852744.0,449592.0],
            "1484901120":[2852928.0,449400.0]
        }
    }
}
{% endhighlight %}

### Fetch Samples of specific AWS Account

#### Required Parameters:

amazon_account_id
: ID of an AWS account to which opsworks stack belongs

idvs
: It is a list of ids(unique for every opsworks stack)

*idv is a combination of region \| opsworks stack id\|

eg. us-east-1\|2a28e197-3e6c-4ebc-99b7-e183d47ad627\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/opsworks.json -d '{ "amazon_account_id":<Amazon Account ID>,"idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "601337641757|us-east-1|ffd7f8f4-1d34-47ed-96b3-ea0ad505ffef|":{
        "c":{
            "1484899440":0.9997,
            "1484899500":0.9997,
            "1484899560":0.9997,
            "1484899620":0.9963,
            "1484899680":0.9997,
            "1484899740":0.9997,
            "1484899800":0.9997,
            "1484899860":0.9997,
            "1484899920":0.9997,
            "1484899980":0.9997,
            "1484900040":0.9997,
            "1484900100":0.998,
            "1484900160":0.9997,
            "1484900220":0.9997,
            "1484900280":0.9997,
            "1484900340":0.9997,
            "1484900400":0.998,
            "1484900460":0.9997,
            "1484900520":0.9997,
            "1484900580":0.9963,
            "1484900640":0.9947,
            "1484900700":0.9963,
            "1484900760":0.9963,
            "1484900820":0.9997,
            "1484900880":0.9997,
            "1484900940":0.9997,
            "1484901000":0.9997,
            "1484901060":0.9997,
            "1484901120":0.9997
        },
        "l":{
            "1484899440":0.0,
            "1484899500":0.0,
            "1484899560":0.0,
            "1484899620":0.0,
            "1484899680":0.0,
            "1484899740":0.0,
            "1484899800":0.0,
            "1484899860":0.0,
            "1484899920":0.0,
            "1484899980":0.0,
            "1484900040":0.0,
            "1484900100":0.0,
            "1484900160":0.0,
            "1484900220":0.0,
            "1484900280":0.0,
            "1484900340":0.0,
            "1484900400":0.0,
            "1484900460":0.0,
            "1484900520":0.0,
            "1484900580":0.0,
            "1484900640":0.0,
            "1484900700":0.0,
            "1484900760":0.0,
            "1484900820":0.0,
            "1484900880":0.0,
            "1484900940":0.0,
            "1484901000":0.0,
            "1484901060":0.0,
            "1484901120":0.0
        },
        "m":{
            "1484899440":[2852872.0,449784.0],
            "1484899500":[2852932.0,449724.0],
            "1484899560":[2852248.0,450388.0],
            "1484899620":[2850172.0,452464.0],
            "1484899680":[2851228.0,451404.0],
            "1484899740":[2851504.0,451124.0],
            "1484899800":[2851380.0,451236.0],
            "1484899860":[2851260.0,451348.0],
            "1484899920":[2851384.0,451220.0],
            "1484899980":[2851944.0,450652.0],
            "1484900040":[2852484.0,450108.0],
            "1484900100":[2852748.0,449836.0],
            "1484900160":[2851564.0,451008.0],
            "1484900220":[2851380.0,451188.0],
            "1484900280":[2851632.0,450932.0],
            "1484900340":[2851940.0,450620.0],
            "1484900400":[2851444.0,451108.0],
            "1484900460":[2851816.0,450724.0],
            "1484900520":[2851324.0,451212.0],
            "1484900580":[2850932.0,451592.0],
            "1484900640":[2850452.0,452020.0],
            "1484900700":[2850620.0,451800.0],
            "1484900760":[2850144.0,452212.0],
            "1484900820":[2851816.0,450524.0],
            "1484900880":[2852684.0,449656.0],
            "1484900940":[2852684.0,449656.0],
            "1484901000":[2852680.0,449660.0],
            "1484901060":[2852744.0,449592.0],
            "1484901120":[2852928.0,449400.0]
        }
    }
}
{% endhighlight %}

---

## Route53

This is an API used to get samples of one or more route53 health checks

### Route53 Sample Keys
{% highlight sh %}
Key name                         Valid combinations

Health                           s
Health percentage                h
{% endhighlight %}

### Fetch Samples from all AWS Accounts

#### Required Parameters:

overview
: Only existence of key is required

idvs
: It is a list of ids(unique for every route53 health check)

*idv is a combination of Amazon Account Number \| region \| route53 health check id \|

eg. 123456789001\|us-east-1\|e761288a-970f-4617-915c-ag55f0844cc6\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/route53.json -d '{ "overview":"overview","idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|e761288a-970f-4617-915c-af55f0854cc6|":{
        "s":{
            "1484899500":0,
            "1484899560":0,
            "1484899620":0,
            "1484899680":0,
            "1484899740":0,
            "1484899800":0,
            "1484899860":0,
            "1484899920":0,
            "1484899980":0,
            "1484900040":0,
            "1484900100":0,
            "1484900160":0,
            "1484900220":0,
            "1484900280":0,
            "1484900340":0,
            "1484900400":0,
            "1484900460":0,
            "1484900520":0,
            "1484900580":0,
            "1484900640":0,
            "1484900700":0,
            "1484900760":0,
            "1484900820":0,
            "1484900880":0,
            "1484900940":0,
            "1484901000":0,
            "1484901060":0,
            "1484901120":0
        },
        "h":{
            "1484899500":0.0,
            "1484899560":0.0,
            "1484899620":0.0,
            "1484899680":0.0,
            "1484899740":0.0,
            "1484899800":0.0,
            "1484899860":0.0,
            "1484899920":0.0,
            "1484899980":0.0,
            "1484900040":0.0,
            "1484900100":0.0,
            "1484900160":0.0,
            "1484900220":0.0,
            "1484900280":0.0,
            "1484900340":0.0,
            "1484900400":0.0,
            "1484900460":0.0,
            "1484900520":0.0,
            "1484900580":0.0,
            "1484900640":0.0,
            "1484900700":0.0,
            "1484900760":0.0,
            "1484900820":0.0,
            "1484900880":0.0,
            "1484900940":0.0,
            "1484901000":0.0,
            "1484901060":0.0,
            "1484901120":0.0
        }
    }
}
{% endhighlight %}

### Fetch Samples of specific AWS Account

#### Required Parameters:

amazon_account_id
: ID of an AWS account to which route53 health check belongs

idvs
: It is a list of ids(unique for every route53 health check)

*idv is a combination of region \| route53 health check id \|

eg. us-east-1\|e761288a-970f-4617-915c-ag55f0844cc6\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/route53.json -d '{ "amazon_account_id":<Amazon Account ID>,"idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|e761288a-970f-4617-915c-af55f0854cc6|":{
        "s":{
            "1484899500":0,
            "1484899560":0,
            "1484899620":0,
            "1484899680":0,
            "1484899740":0,
            "1484899800":0,
            "1484899860":0,
            "1484899920":0,
            "1484899980":0,
            "1484900040":0,
            "1484900100":0,
            "1484900160":0,
            "1484900220":0,
            "1484900280":0,
            "1484900340":0,
            "1484900400":0,
            "1484900460":0,
            "1484900520":0,
            "1484900580":0,
            "1484900640":0,
            "1484900700":0,
            "1484900760":0,
            "1484900820":0,
            "1484900880":0,
            "1484900940":0,
            "1484901000":0,
            "1484901060":0,
            "1484901120":0
        },
        "h":{
            "1484899500":0.0,
            "1484899560":0.0,
            "1484899620":0.0,
            "1484899680":0.0,
            "1484899740":0.0,
            "1484899800":0.0,
            "1484899860":0.0,
            "1484899920":0.0,
            "1484899980":0.0,
            "1484900040":0.0,
            "1484900100":0.0,
            "1484900160":0.0,
            "1484900220":0.0,
            "1484900280":0.0,
            "1484900340":0.0,
            "1484900400":0.0,
            "1484900460":0.0,
            "1484900520":0.0,
            "1484900580":0.0,
            "1484900640":0.0,
            "1484900700":0.0,
            "1484900760":0.0,
            "1484900820":0.0,
            "1484900880":0.0,
            "1484900940":0.0,
            "1484901000":0.0,
            "1484901060":0.0,
            "1484901120":0.0
        }
    }
}
{% endhighlight %}

---

## SQS

This is an API used to get samples of one or more SQS Queues

### SQS Sample Keys
{% highlight sh %}
Key name                         Valid combinations

Message available                r
Message sent/receive             l
{% endhighlight %}

### Fetch Samples from all AWS Accounts

#### Required Parameters:

overview
: Only existence of key is required

idvs
: It is a list of ids(unique for every SQS queue)

*idv is a combination of Amazon Account Number \| region \| sqs queue name \|

eg. 123456789001\|us-east-1\|test-sqs\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/sqs.json -d '{ "overview":"overview","idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|test-sqs|":{
        "l":{
            "1484899500":[0,0], # [sent, received]
            "1484899800":[9,0],
            "1484900100":[7,0],
            "1484900400":[0,0],
            "1484900700":[9,0],
            "1484901000":[0,0]
        },
        "r":{
            "1484899500":[5679,0], # [visible, not_visible]
            "1484899800":[5678,0],
            "1484900100":[5678,0],
            "1484900400":[5678,0],
            "1484900700":[5681,0],
            "1484901000":[5679,0]
        }
    }
}
{% endhighlight %}

### Fetch Samples of specific AWS Account

#### Required Parameters:

amazon_account_idl
: ID of an AWS account to which sqs queue belongs

idvs
: It is a list of ids(unique for every sqs queue)

*idv is a combination of region \| sqs queue name \|

eg. us-east-1\|test-sqs\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/sqs.json -d '{ "amazon_account_id":<Amazon Account ID>,"idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|test-sqs|":{
        "l":{
            "1484899500":[0,0],
            "1484899800":[9,0],
            "1484900100":[7,0],
            "1484900400":[0,0],
            "1484900700":[9,0],
            "1484901000":[0,0]
        },
        "r":{
            "1484899500":[5679,0],
            "1484899800":[5678,0],
            "1484900100":[5678,0],
            "1484900400":[5678,0],
            "1484900700":[5681,0],
            "1484901000":[5679,0]
        }
    }
}
{% endhighlight %}

---

## SNS

This is an API used to get samples of one or more SNS topics

### SNS Sample Keys
{% highlight sh %}
Key name                         Valid combinations

Notifications                    r
Message size                     l
Message published                c
{% endhighlight %}

### Fetch Samples from all AWS Accounts

#### Required Parameters:

overview
: Only existence of key is required

idvs
: It is a list of ids(unique for every SNS topic)

*idv is a combination of Amazon Account Number \| region \| SNS topic name \|

eg. 123456789001\|us-east-1\|test-sns\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/sns.json -d '{ "overview":"overview","idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|test-sns|":{
        "c":{
            "1484899800":9,
            "1484900100":7,
            "1484900700":9
        },
        "l":{
            "1484899800":193,
            "1484900100":197,
            "1484900700":207
        },
        "r":{
            "1484899800":[9,0], # [delivered, failed]
            "1484900100":[7,0],
            "1484900700":[9,0]
        }
    }
}
{% endhighlight %}

### Fetch Samples of specific AWS Account

#### Required Parameters:

amazon_account_id
: ID of an AWS account to which SNS topic belongs

idvs
: It is a list of ids(unique for every SNS topic)

*idv is a combination of region \| SNS topic name \|

eg. us-east-1\|test-sns\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/sns.json -d '{ "amazon_account_id":<Amazon Account ID>,"idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|test-sns|":{
        "c":{
            "1484899800":9,
            "1484900100":7,
            "1484900700":9
        },
        "l":{
            "1484899800":193,
            "1484900100":197,
            "1484900700":207
        },
        "r":{
            "1484899800":[9,0],
            "1484900100":[7,0],
            "1484900700":[9,0]
        }
    }
}
{% endhighlight %}

---

## EMR

This is an API used to get samples of one or more emr clusters

### EMR Sample Keys
{% highlight sh %}
Key name                                            Valid combinations

Apps Failed                                         f
Apps Running                                        r
Core Nodes Running read & Core Nodes Pending        c
Live Task Trackers & Live Data Nodes                l
{% endhighlight %}

### Fetch Samples from all AWS Accounts

#### Required Parameters:

overview
: Only existence of key is required

idvs
: It is a list of ids(unique for every emr cluster)

*idv is a combination of Amazon Account Number \| region \| emr cluster id \|

eg. 123456789001\|us-east-1\|test-cluster\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/emr.json -d '{ "overview":"overview","idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|j-2C4W4A2B3UW9X|":{
        "f":{
            "1485268620":0,
            "1485268920":0,
            "1485269220":0,
            "1485269520":0,
            "1485269820":0
        },
        "r":{
            "1485268620":0,
            "1485268920":0,
            "1485269220":0,
            "1485269520":0,
            "1485269820":0
        },
        "c":{
            "1485268620":[null,null], # [core_pending, core_run]
            "1485268920":[null,null],
            "1485269220":[null,null],
            "1485269520":[null,null],
            "1485269820":[null,null]
        },
        "l":{
            "1485268620":[1,null], # [live_task, live_data]
            "1485268920":[1,null],
            "1485269220":[1,null],
            "1485269520":[1,null],
            "1485269820":[1,null]
        }
    }
}
{% endhighlight %}

### Fetch Samples of specific AWS Account

#### Required Parameters:

amazon_account_id
: ID of an AWS account to which emr cluster belongs

idvs
: It is a list of ids(unique for every emr cluster)

*idv is a combination of region \| emr cluster id \|

eg. us-east-1\|test-cluster\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/emr.json -d '{ "amazon_account_id":<Amazon Account ID>,"idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|j-2C4W4A2B3UW9X|":{
        "f":{
            "1485268620":0,
            "1485268920":0,
            "1485269220":0,
            "1485269520":0,
            "1485269820":0
        },
        "r":{
            "1485268620":0,
            "1485268920":0,
            "1485269220":0,
            "1485269520":0,
            "1485269820":0
        },
        "c":{
            "1485268620":[null,null],
            "1485268920":[null,null],
            "1485269220":[null,null],
            "1485269520":[null,null],
            "1485269820":[null,null]
        },
        "l":{
            "1485268620":[1,null],
            "1485268920":[1,null],
            "1485269220":[1,null],
            "1485269520":[1,null],
            "1485269820":[1,null]
        }
    }
}
{% endhighlight %}

---

## Machine Learning

This is an API used to get samples of one or more Machine Learning models

### Machine Learning Sample Keys
{% highlight sh %}
Key name                         Valid combinations

Predict Count                    c
Predict Failure Count            f
{% endhighlight %}

### Fetch Samples from all AWS Accounts

#### Required Parameters:

overview
: Only existence of key is required

idvs
: It is a list of ids(unique for every Machine Learning model)

*idv is a combination of Amazon Account Number \| region \| Machine Learning Model name \|

eg. 123456789001\|us-east-1\|ml-KrgrdKta03v\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/ml.json -d '{ "overview":"overview","idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|ml-KrgrdKta03v|RealTimePredictions|":{
        "c":{
            "1485269340":0,
            "1485269700":0,
            "1485270000":0,
            "1485270300":0,
            "1485270660":0
        },
        "f":{}
    }
}
{% endhighlight %}

### Fetch Samples of specific AWS Account

#### Required Parameters:

amazon_account_id
: ID of an AWS account to which Machine Learning Model belongs

idvs
: It is a list of ids(unique for every Machine Learning Model)

*idv is a combination of region \| Machine Learning Model name \|

eg. us-east-1\|ml-KrgrdKta03v\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/ml.json -d '{ "amazon_account_id":<Amazon Account ID>,"idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|ml-KrgrdKta03v|RealTimePredictions|":{
        "c":{
            "1485269340":0,
            "1485269700":0,
            "1485270000":0,
            "1485270300":0,
            "1485270660":0
        },
        "f":{}
    }
}
{% endhighlight %}

---

## Redshift

This is an API used to get samples of one or more redshift clusters

### Redshift Sample Keys
{% highlight sh %}
Key name                         Valid combinations

CPU Utilization                  c
Database Connections             l
Disk                             d
Others                           r
{% endhighlight %}

### Fetch Samples from all AWS Accounts

#### Required Parameters:

overview
: Only existence of key is required

idvs
: It is a list of ids(unique for every Redshift clusters)

*idv is a combination of Amazon Account Number \| region \| Redshift cluster name \|

eg. 123456789001\|us-east-1\|awstest\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/redshift.json -d '{ "overview":"overview","idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|awstest|Shared|":{
        "c":{
            "1485269340":0.008,
            "1485269400":0.007,
            "1485269460":0.006,
            "1485269520":0.007,
            "1485269580":0.006,
            "1485269640":0.008,
            "1485269700":0.007,
            "1485269760":0.007,
            "1485269820":0.007,
            "1485269880":0.006,
            "1485269940":0.008,
            "1485270000":0.006,
            "1485270180":0.006,
            "1485270240":0.008,
            "1485270300":0.007,
            "1485270360":0.006,
            "1485270420":0.007,
            "1485270480":0.006,
            "1485270540":0.008,
            "1485270600":0.007,
            "1485270660":0.006,
            "1485270720":0.008,
            "1485270780":0.007,
            "1485270840":0.008,
            "1485270900":0.006,
            "1485270960":0.008
        },
        "l":{
            "1485269340":0,
            "1485269400":0,
            "1485269460":0,
            "1485269520":0,
            "1485269580":0,
            "1485269640":0,
            "1485269700":0,
            "1485269760":0,
            "1485269820":0,
            "1485269880":0,
            "1485269940":0,
            "1485270000":0,
            "1485270060":0,
            "1485270180":0,
            "1485270240":0,
            "1485270300":0,
            "1485270360":0,
            "1485270420":0,
            "1485270480":0,
            "1485270540":0,
            "1485270600":0,
            "1485270660":0,
            "1485270720":0,
            "1485270780":0,
            "1485270840":0,
            "1485270900":0,
            "1485270960":0,
            "1485271020":0
        },
        "r":{
            "1485269340":[1,0], # [health_status, maint_mode]
            "1485269400":[1,0],
            "1485269460":[1,0],
            "1485269520":[1,0],
            "1485269580":[1,0],
            "1485269640":[1,0],
            "1485269700":[1,0],
            "1485269760":[1,0],
            "1485269820":[1,0],
            "1485269880":[1,0],
            "1485269940":[1,0],
            "1485270000":[1,0],
            "1485270060":[1,0],
            "1485270180":[1,0],
            "1485270240":[1,0],
            "1485270300":[1,0],
            "1485270360":[1,0],
            "1485270420":[1,0],
            "1485270480":[1,0],
            "1485270540":[1,0],
            "1485270600":[1,0],
            "1485270660":[1,0],
            "1485270720":[1,0],
            "1485270780":[1,0],
            "1485270840":[1,0],
            "1485270900":[1,0],
            "1485270960":[1,0],
            "1485271020":[1,0]
        },
        "d":{
            "1485269340":0.00032,
            "1485269400":0.00032,
            "1485269460":0.00032,
            "1485269520":0.00032,
            "1485269580":0.00032,
            "1485269640":0.00032,
            "1485269700":0.00032,
            "1485269760":0.00032,
            "1485269820":0.00032,
            "1485269880":0.00032,
            "1485269940":0.00032,
            "1485270000":0.00032,
            "1485270060":0.00032,
            "1485270180":0.00032,
            "1485270240":0.00032,
            "1485270300":0.00032,
            "1485270360":0.00032,
            "1485270420":0.00032,
            "1485270480":0.00032,
            "1485270540":0.00032,
            "1485270600":0.00032,
            "1485270660":0.00032,
            "1485270720":0.00032,
            "1485270780":0.00032,
            "1485270840":0.00032,
            "1485270900":0.00032,
            "1485270960":0.00032,
            "1485271020":0.00032
        }
    }
}
{% endhighlight %}

### Fetch Samples of specific AWS Account

#### Required Parameters:

amazon_account_id
: ID of an AWS account to which redshift cluster belongs

idvs
: It is a list of ids(unique for every redshift cluster)

*idv is a combination of region \| redshift cluster name \|

eg. us-east-1\|awstest\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/redshift.json -d '{ "amazon_account_id":<Amazon Account ID>,"idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|awstest|Shared|":{
        "c":{
            "1485269340":0.008,
            "1485269400":0.007,
            "1485269460":0.006,
            "1485269520":0.007,
            "1485269580":0.006,
            "1485269640":0.008,
            "1485269700":0.007,
            "1485269760":0.007,
            "1485269820":0.007,
            "1485269880":0.006,
            "1485269940":0.008,
            "1485270000":0.006,
            "1485270180":0.006,
            "1485270240":0.008,
            "1485270300":0.007,
            "1485270360":0.006,
            "1485270420":0.007,
            "1485270480":0.006,
            "1485270540":0.008,
            "1485270600":0.007,
            "1485270660":0.006,
            "1485270720":0.008,
            "1485270780":0.007,
            "1485270840":0.008,
            "1485270900":0.006,
            "1485270960":0.008
        },
        "l":{
            "1485269340":0,
            "1485269400":0,
            "1485269460":0,
            "1485269520":0,
            "1485269580":0,
            "1485269640":0,
            "1485269700":0,
            "1485269760":0,
            "1485269820":0,
            "1485269880":0,
            "1485269940":0,
            "1485270000":0,
            "1485270060":0,
            "1485270180":0,
            "1485270240":0,
            "1485270300":0,
            "1485270360":0,
            "1485270420":0,
            "1485270480":0,
            "1485270540":0,
            "1485270600":0,
            "1485270660":0,
            "1485270720":0,
            "1485270780":0,
            "1485270840":0,
            "1485270900":0,
            "1485270960":0,
            "1485271020":0
        },
        "r":{
            "1485269340":[1,0],
            "1485269400":[1,0],
            "1485269460":[1,0],
            "1485269520":[1,0],
            "1485269580":[1,0],
            "1485269640":[1,0],
            "1485269700":[1,0],
            "1485269760":[1,0],
            "1485269820":[1,0],
            "1485269880":[1,0],
            "1485269940":[1,0],
            "1485270000":[1,0],
            "1485270060":[1,0],
            "1485270180":[1,0],
            "1485270240":[1,0],
            "1485270300":[1,0],
            "1485270360":[1,0],
            "1485270420":[1,0],
            "1485270480":[1,0],
            "1485270540":[1,0],
            "1485270600":[1,0],
            "1485270660":[1,0],
            "1485270720":[1,0],
            "1485270780":[1,0],
            "1485270840":[1,0],
            "1485270900":[1,0],
            "1485270960":[1,0],
            "1485271020":[1,0]
        },
        "d":{
            "1485269340":0.00032,
            "1485269400":0.00032,
            "1485269460":0.00032,
            "1485269520":0.00032,
            "1485269580":0.00032,
            "1485269640":0.00032,
            "1485269700":0.00032,
            "1485269760":0.00032,
            "1485269820":0.00032,
            "1485269880":0.00032,
            "1485269940":0.00032,
            "1485270000":0.00032,
            "1485270060":0.00032,
            "1485270180":0.00032,
            "1485270240":0.00032,
            "1485270300":0.00032,
            "1485270360":0.00032,
            "1485270420":0.00032,
            "1485270480":0.00032,
            "1485270540":0.00032,
            "1485270600":0.00032,
            "1485270660":0.00032,
            "1485270720":0.00032,
            "1485270780":0.00032,
            "1485270840":0.00032,
            "1485270900":0.00032,
            "1485270960":0.00032,
            "1485271020":0.00032
        }
    }
}
{% endhighlight %}

---

## Cloudsearch

This is an API used to get samples of one or more Cloudsearch domain

### Cloudsearch Sample Keys
{% highlight sh %}
Key name                         Valid combinations

Successful Requests              c
Searchable Documents             l
Index Utilization                r
Partitions                       o
{% endhighlight %}

### Fetch Samples from all AWS Accounts

#### Required Parameters:

overview
: Only existence of key is required

idvs
: It is a list of ids(unique for every Cloudsearch domain)

*idv is a combination of Amazon Account Number \| region \| Cloudsearch domain name \|

eg. 123456789001\|us-east-1\|awstest\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/cloudsearch.json -d '{ "overview":"overview","idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|awstest|123456789002|":{
        "c":{
            "1485269460":0,
            "1485269520":0,
            "1485269580":0,
            "1485269640":0,
            "1485269700":0,
            "1485269760":0,
            "1485269820":0,
            "1485269880":0,
            "1485269940":0,
            "1485270000":0,
            "1485270060":0,
            "1485270120":0,
            "1485270180":0,
            "1485270240":0,
            "1485270300":0,
            "1485270360":0,
            "1485270420":0,
            "1485270480":0,
            "1485270540":0,
            "1485270600":0,
            "1485270660":0,
            "1485270720":0,
            "1485270780":0,
            "1485270840":0,
            "1485270900":0,
            "1485270960":0,
            "1485271020":0
        },
        "l":{
            "1485269460":0,
            "1485269520":0,
            "1485269580":0,
            "1485269640":0,
            "1485269700":0,
            "1485269760":0,
            "1485269820":0,
            "1485269880":0,
            "1485269940":0,
            "1485270000":0,
            "1485270060":0,
            "1485270120":0,
            "1485270180":0,
            "1485270240":0,
            "1485270300":0,
            "1485270360":0,
            "1485270420":0,
            "1485270480":0,
            "1485270540":0,
            "1485270600":0,
            "1485270660":0,
            "1485270720":0,
            "1485270780":0,
            "1485270840":0,
            "1485270900":0,
            "1485270960":0,
            "1485271020":0
        },
        "r":{
            "1485269460":0,
            "1485269520":0,
            "1485269580":0,
            "1485269640":0,
            "1485269700":0,
            "1485269760":0,
            "1485269820":0,
            "1485269880":0,
            "1485269940":0,
            "1485270000":0,
            "1485270060":0,
            "1485270120":0,
            "1485270180":0,
            "1485270240":0,
            "1485270300":0,
            "1485270360":0,
            "1485270420":0,
            "1485270480":0,
            "1485270540":0,
            "1485270600":0,
            "1485270660":0,
            "1485270720":0,
            "1485270780":0,
            "1485270840":0,
            "1485270900":0,
            "1485270960":0,
            "1485271020":0
        },
        "o":{
            "1485269460":1,
            "1485269520":1,
            "1485269580":1,
            "1485269640":1,
            "1485269700":1,
            "1485269760":1,
            "1485269820":1,
            "1485269880":1,
            "1485269940":1,
            "1485270000":1,
            "1485270060":1,
            "1485270120":1,
            "1485270180":1,
            "1485270240":1,
            "1485270300":1,
            "1485270360":1,
            "1485270420":1,
            "1485270480":1,
            "1485270540":1,
            "1485270600":1,
            "1485270660":1,
            "1485270720":1,
            "1485270780":1,
            "1485270840":1,
            "1485270900":1,
            "1485270960":1,
            "1485271020":1
        }
    }
}
{% endhighlight %}

### Fetch Samples of specific AWS Account

#### Required Parameters:

amazon_account_id
: ID of an AWS account to which Cloudsearch domain belongs

idvs
: It is a list of ids(unique for every Cloudsearch domain)

*idv is a combination of region \| Cloudsearch domain name \|

eg. us-east-1\|awstest\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/cloudsearch.json -d '{ "amazon_account_id":<Amazon Account ID>,"idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|awstest|123456789002|":{
        "c":{
            "1485269460":0,
            "1485269520":0,
            "1485269580":0,
            "1485269640":0,
            "1485269700":0,
            "1485269760":0,
            "1485269820":0,
            "1485269880":0,
            "1485269940":0,
            "1485270000":0,
            "1485270060":0,
            "1485270120":0,
            "1485270180":0,
            "1485270240":0,
            "1485270300":0,
            "1485270360":0,
            "1485270420":0,
            "1485270480":0,
            "1485270540":0,
            "1485270600":0,
            "1485270660":0,
            "1485270720":0,
            "1485270780":0,
            "1485270840":0,
            "1485270900":0,
            "1485270960":0,
            "1485271020":0
        },
        "l":{
            "1485269460":0,
            "1485269520":0,
            "1485269580":0,
            "1485269640":0,
            "1485269700":0,
            "1485269760":0,
            "1485269820":0,
            "1485269880":0,
            "1485269940":0,
            "1485270000":0,
            "1485270060":0,
            "1485270120":0,
            "1485270180":0,
            "1485270240":0,
            "1485270300":0,
            "1485270360":0,
            "1485270420":0,
            "1485270480":0,
            "1485270540":0,
            "1485270600":0,
            "1485270660":0,
            "1485270720":0,
            "1485270780":0,
            "1485270840":0,
            "1485270900":0,
            "1485270960":0,
            "1485271020":0
        },
        "r":{
            "1485269460":0,
            "1485269520":0,
            "1485269580":0,
            "1485269640":0,
            "1485269700":0,
            "1485269760":0,
            "1485269820":0,
            "1485269880":0,
            "1485269940":0,
            "1485270000":0,
            "1485270060":0,
            "1485270120":0,
            "1485270180":0,
            "1485270240":0,
            "1485270300":0,
            "1485270360":0,
            "1485270420":0,
            "1485270480":0,
            "1485270540":0,
            "1485270600":0,
            "1485270660":0,
            "1485270720":0,
            "1485270780":0,
            "1485270840":0,
            "1485270900":0,
            "1485270960":0,
            "1485271020":0
        },
        "o":{
            "1485269460":1,
            "1485269520":1,
            "1485269580":1,
            "1485269640":1,
            "1485269700":1,
            "1485269760":1,
            "1485269820":1,
            "1485269880":1,
            "1485269940":1,
            "1485270000":1,
            "1485270060":1,
            "1485270120":1,
            "1485270180":1,
            "1485270240":1,
            "1485270300":1,
            "1485270360":1,
            "1485270420":1,
            "1485270480":1,
            "1485270540":1,
            "1485270600":1,
            "1485270660":1,
            "1485270720":1,
            "1485270780":1,
            "1485270840":1,
            "1485270900":1,
            "1485270960":1,
            "1485271020":1
        }
    }
}
{% endhighlight %}

---

## Workspaces

This is an API used to get samples of one or more Workspaces

### Workspaces Sample Keys
{% highlight java %}
Key name                         Valid combinations

Healthy                          a
Unhealthy                        u
Connection Attempts              c
Connection Success               s
Connection Failure               f
Session launch time              l
Latency                          i
Disconnect                       d
{% endhighlight %}

### Fetch Samples from all AWS Accounts

#### Required Parameters:

overview
: Only existence of key is required

idvs
: It is a list of ids(unique for every Workspace)

*idv is a combination of Amazon Account Number \| region \| Workspace id \|

eg. 123456789001\|us-east-1\|d-90673c00b3\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/workspaces.json -d '{ "overview":"overview","idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|d-90673c00b3|":{
        "a":{
            "1485269520":1,
            "1485269640":1,
            "1485269820":1,
            "1485269940":1,
            "1485270120":1,
            "1485270240":1,
            "1485270420":1,
            "1485270540":1,
            "1485270720":1,
            "1485270840":1,
            "1485271020":1
        },
        "u":{
            "1485269520":0,
            "1485269640":0,
            "1485269820":0,
            "1485269940":0,
            "1485270120":0,
            "1485270240":0,
            "1485270420":0,
            "1485270540":0,
            "1485270720":0,
            "1485270840":0,
            "1485271020":0
        },
        "c":{},
        "s":{},
        "f":{},
        "l":{},
        "i":{},
        "d":{}
    }
}
{% endhighlight %}

### Fetch Samples of specific AWS Account

#### Required Parameters:

amazon_account_id
: ID of an AWS account to which Workspace belongs

idvs
: It is a list of ids(unique for every sns topic)

*idv is a combination of region \| Workspaces id \|

eg. us-east-1\|d-90673c00b3\|

#### CURL Command:

{% highlight sh %}
curl -s -XPOST -H "Content-Type: application/json" https://<APIKEY>:U@api.copperegg.com/v2/aws/samples/workspaces.json -d '{ "amazon_account_id":<Amazon Account ID>,"idvs":["<IDV1>","<IDV2>"] }'
{% endhighlight %}

#### CURL Response:

{% highlight ruby %}
{
    "123456789001|us-east-1|d-90673c00b3|":{
        "a":{
            "1485269520":1,
            "1485269640":1,
            "1485269820":1,
            "1485269940":1,
            "1485270120":1,
            "1485270240":1,
            "1485270420":1,
            "1485270540":1,
            "1485270720":1,
            "1485270840":1,
            "1485271020":1
        },
        "u":{
            "1485269520":0,
            "1485269640":0,
            "1485269820":0,
            "1485269940":0,
            "1485270120":0,
            "1485270240":0,
            "1485270420":0,
            "1485270540":0,
            "1485270720":0,
            "1485270840":0,
            "1485271020":0
        },
        "c":{},
        "s":{},
        "f":{},
        "l":{},
        "i":{},
        "d":{}
    }
}
{% endhighlight %}

---
