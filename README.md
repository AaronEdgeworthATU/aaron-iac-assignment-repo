# aaron-iac-assignment-repo
Will be used for assignments given in the IaC for DevOps Pipelines course.

Template file was added. Initial template file is very basic, only provisioning the S3 Bucket to store the webpage index.html.

Making updates to the template.yaml file to include an S3 Bucket policy. Without this there may be security and access risks. The policy will aim to only allow access from a cloud front distribution that I will set up. Also added a "Bucket:" property to my VPC, not sure what it does right now but Im assuming it ensures the VPC that is established will use the S3 Bucket as it's reference.

Setting up the S3 Bucket policy and the CloudFront distribution to allow the webpage to be accessible through cloudfront and not publically.

Having issues with the OAC configuration. The stack is being created successfully but the S3 buckets resources are inaccessible.

Correction to the earlier note about the "Bucket:" property. It is on the bucket policy, not the VPC. It tells the policy which S3 bucket it applies to. The VPC does not control access to the S3 bucket. Access is controlled by the bucket policy and the OAC, so the VPC does not belong in this template and I need to remove it.

Looked into the OAC issue. The stack creates fine but visiting the CloudFront URL gave an Access Denied error. I think the cause is that CloudFormation does not upload files, so the bucket had no index.html in it. Will need to upload the index.html manually after the stack deployment.

I removed WebsiteConfiguration, because it is for the public S3 website endpoint and Im now using Cloudfront and OAC to access. I dont believe I need the VPC for the static website host.
