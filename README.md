### configure profiles in awscli
```
aws configure --profile=red
```
### list buckets
```
aws s3 ls --profile=red
```
### Access to own bucket IAM policy
```
{
  "Version": "2012-10-17",
  "Statement":[{
    "Effect": "Allow",
    "Action": "s3:*",
    "Resource": ["arn:aws:s3:::red.anitta.cloud/*"]
    }
  ]
}
```
### listing own buckets
```
aws s3 ls s3://red.anitta.cloud --profile=red
```
### listing other buckets
```
aws s3 ls s3://blue.anitta.cloud --profile=red
```
### upload file to own bucket
```
aws s3 cp newfile.txt s3://red.anitta.cloud --profile=red
```
###upload file to other bucket
```
aws s3 cp newfile.txt s3://blue.anitta.cloud --profile=red
```
### updated policy to include access to bucket, and objects
```
{
  "Version": "2012-10-17",
  "Statement":[{
    "Effect": "Allow",
    "Action": "s3:*",
    "Resource": [ "arn:aws:s3:::red.anitta.cloud",
                 "arn:aws:s3:::red.anitta.cloud/*"]
    }
  ]
}
```
### updated policy to allow listing all buckets
```
{
  "Version": "2012-10-17",
  "Statement":[
   {
    "Sid": "Listingownbucket",
    "Effect": "Allow",
    "Action": "s3:*",
    "Resource": [ "arn:aws:s3:::red.anitta.cloud",
                  "arn:aws:s3:::red.anitta.cloud/*"]
   },
   {
    "Sid": "Listingallbuckets",
    "Effect": "Allow",
    "Action": "s3:ListAllMyBuckets",
    "Resource": "*"
   }
  ]
}
```
### Denies listing and operations on own buckets and allow listing all buckets
```
{
  "Version": "2012-10-17",
  "Statement":[
   {
    "Sid": "Listingownbucket",
    "Effect": "Deny",
    "Action": "s3:*",
    "Resource": [ "arn:aws:s3:::red.anitta.cloud",
                  "arn:aws:s3:::red.anitta.cloud/*"]
   },
   {
    "Sid": "Listingallbuckets",
    "Effect": "Allow",
    "Action": "s3:ListAllMyBuckets",
    "Resource": "*"
   }
  ]
}

```
### Allow any action on specific buckets
```
{
  "Version": "2012-10-17",
  "Statement":[
   {
    "Sid": "Listing own bucket",
    "Effect": "Allow",
    "Action": "s3:*",
    "Resource": [ "arn:aws:s3:::a-bucket",
                  "arn:aws:s3:::a-bucket/*",
                  "arn:aws:s3:::b-bucket",
                  "arn:aws:s3:::b-bucket/*",
                  "arn:aws:s3:::c-bucket",
                  "arn:aws:s3:::c-bucket/*"
                ]
   }
  ]
}
```
### bucket policy to allow IAM user to do actions in specific buckets
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": ["arn:aws:iam::082897113543:user/red"]
      },
      "Action": "s3:*",
      "Resource": ["arn:aws:s3:::red.anitta.cloud",
                   "arn:aws:s3:::red.anitta.cloud/*"
                  ]
    }
  ]
}
```
### Just list all buckets in IAM policy . Might need to add it alongside ^^
```
{
  "Version": "2012-10-17",
  "Statement":[
   {
    "Sid": "Listingallbuckets",
    "Effect": "Allow",
    "Action": "s3:ListAllMyBuckets",
    "Resource": "*"
   }
  ]
}
```
### Adds multiple users access to the same bucket

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": ["arn:aws:iam::082897113543:user/red",
                "arn:aws:iam::082897113543:user/blue"]
      },
      "Action": "s3:*",
      "Resource": ["arn:aws:s3:::backup.anitta.cloud",
                   "arn:aws:s3:::backup.anitta.cloud/*"
                  ]
    }
  ]
}

```
#### public bucket policy
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Stmt1405592139000",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": [
                "arn:aws:s3:::study.anitta.cloud/*",
                "arn:aws:s3:::study.anitta.cloud"
            ]
        }
    ]
}
```
#### Make versions public as well
```
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Effect": "Allow",
			"Principal": "*",
			"Action": [
			          "s3:GetObject",
			          "s3:GetObjectVersion"
			          ],
			"Resource": [
				"arn:aws:s3:::version.anitta.cloud/*",
				"arn:aws:s3:::version.anitta.cloud"
			]
		}
	]
}
```
#### Remote Bucket Details
```
Bucket Name : s3website.trainingdevops.cloud  

Bucket Policy :

{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::082897113543:user/red"
            },
            "Action": "s3:*",
            "Resource": [
                "arn:aws:s3:::s3website.trainingdevops.cloud",
                "arn:aws:s3:::s3website.trainingdevops.cloud/*"
            ]
        }
    ]
}
```
#### Local Iam User Policy
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:*"
            ],
            "Resource": [
                "arn:aws:s3:::s3website.trainingdevops.cloud",
                "arn:aws:s3:::s3website.trainingdevops.cloud/*"
            ]
        }
    ]
}
```
