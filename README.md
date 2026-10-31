# aaron-iac-assignment-repo
Will be used for assignments given in the IaC for DevOps Pipelines course.

Template file was added. Initial template file is very basic, only provisioning the S3 Bucket to store the webpage index.html.

Making updates to the template.yaml file to include an S3 Bucket policy. Without this there may be security and access risks. The policy will aim to only allow access from a cloud front distribution that I will set up. Also added a "Bucket:" property to my VPC, not sure what it does right now but Im assuming it ensures the VPC that is established will use the S3 Bucket as it's reference.

Setting up the S3 Bucket policy and the CloudFront distribution to allow the webpage to be accessible through cloudfront and not publically.