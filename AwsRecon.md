## External and Internal Recon

#### S3 enum

- External/Public
1 - https://cloud.hacktricks.xyz/pentesting-cloud/aws-security/aws-unauthenticated-enum-access/aws-s3-unauthenticated-enum

2 - Discovering Bucket Names:

There are many ways to discover the names of Buckets. One of the easiest ways is when a company embeds content hosted in S3 on their website. Images, PDFs, etc., can all be hosted cheaply in S3 and linked from another site. These links will look like this: 
- ```http://BUCKETNAME.s3.amazonaws.com/FILENAME.ext``` or ```http://s3.amazonaws.com/BUCKETNAME/FILENAME.ext```

3 - Find public IP to see if it is s3 aws:
  - ```$ dig sub.domain.com``` and ```$ nslookup IP```
  - ```$ dig +nocmd flaws.cloud any +multiline +noall +answer``` and ```$ nslookup IP```

4 - Enumerate Bucket:
  - To test the openness of the bucket a user can just enter the URL in their web browser. A private bucket will respond with "Access Denied". A public bucket will list the first 1,000 objects that have been stored.

5 - Listing the Contents of Buckets:
  - ```$ curl http://BUCKETNAME.s3.amazonaws.com/```
  - ```$ aws s3 ls s3://irs-form-990/ --no-sign-request``` 

6 - Downloading Objects:
  - ```$ curl http://irs-form-990.s3.amazonaws.com/201101319349101615_public.xml```
  - ```$ aws s3 cp s3://irs-form-990/201101319349101615_public.xml . --no-sign-request```

7 - S3 misconfig serie:

1. http://flaws.cloud/
2. http://flaws.cloud/hint1.html
3. http://flaws.cloud/hint2.html
4. http://level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud/
5. http://level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud/hint1.html
6. http://level3-9afd3927f195e10225021a578e6f78df.flaws.cloud/
7. http://level3-9afd3927f195e10225021a578e6f78df.flaws.cloud/hint1.html
8. http://level4-1156739cfb264ced6de514971a4bef68.flaws.cloud/
9. http://level4-1156739cfb264ced6de514971a4bef68.flaws.cloud/hint1.html
10. http://level4-1156739cfb264ced6de514971a4bef68.flaws.cloud/hint2.html
11. http://level4-1156739cfb264ced6de514971a4bef68.flaws.cloud/hint3.html
12. http://level5-d2891f604d2061b6977c2481b0c8333e.flaws.cloud/243f422c/hint2.html
13. http://level5-d2891f604d2061b6977c2481b0c8333e.flaws.cloud/243f422c/hint3.html
14. http://level6-cc4c404a8a8b876167f5e70a7d8c9880.flaws.cloud/ddcc78ff/
15. 

#### IAM

1 - https://hackingthe.cloud/aws/general-knowledge/using_stolen_iam_credentials/
  - https://cloud.hacktricks.xyz/pentesting-cloud/aws-security/aws-basic-information#cli-authentication

When you find credentials to AWS, you can add them to your AWS Profile in the AWS CLI. For this, you use the command:

https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html#cli-configure-files-using-profiles

```aws configure --profile PROFILENAME```

This command will add entries to the .aws/config and .aws/credentials files in your user's home directory.

```ProTip: Never store a set of access keys in the [default] profile. Doing so forces you always to specify a profile and never accidentally run a command against an account you don't intend to.```

2 - A few other common AWS reconnaissance techniques are:

  - Finding the Account ID belonging to an access key:
  - ```aws sts get-access-key-info --access-key-id AKIAEXAMPLE```

  - Determining the Username the access key you're using belongs to
  - ```aws sts get-caller-identity --profile PROFILENAME```

  - Listing all the EC2 instances running in an account
  - ```aws ec2 describe-instances --output text --profile PROFILENAME```

  - Listing all the EC2 instances running in an account in a different region
  - ```aws ec2 describe-instances --output text --region us-east-1 --profile PROFILENAME```

