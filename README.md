# aaron-iac-assignment-repo
Will be used for assignments given in the IaC for DevOps Pipelines course.

Template file was added. Initial template file is very basic, only provisioning the S3 Bucket to store the webpage index.html.

Making updates to the template.yaml file to include an S3 Bucket policy. Without this there may be security and access risks. The policy will aim to only allow access from a cloud front distribution that I will set up. Also added a "Bucket:" property to my VPC, not sure what it does right now but Im assuming it ensures the VPC that is established will use the S3 Bucket as it's reference.

Setting up the S3 Bucket policy and the CloudFront distribution to allow the webpage to be accessible through cloudfront and not publically.

Having issues with the OAC configuration. The stack is being created successfully but the S3 buckets resources are inaccessible.

Correction to the earlier note about the "Bucket:" property. It is on the bucket policy, not the VPC. It tells the policy which S3 bucket it applies to. The VPC does not control access to the S3 bucket. Access is controlled by the bucket policy and the OAC, so the VPC does not belong in this template and I need to remove it.

Looked into the OAC issue. The stack creates fine but visiting the CloudFront URL gave an Access Denied error. I think the cause is that CloudFormation does not upload files, so the bucket had no index.html in it. Will need to upload the index.html manually after the stack deployment.

I removed WebsiteConfiguration, because it is for the public S3 website endpoint and Im now using Cloudfront and OAC to access. I dont believe I need the VPC for the static website host.

Uploading the new yaml file to include the skeleton of the three tier architecture. Initally establishing the VPC that I had unnessisarily included in the static website yaml template. The VPC is being established with two subets. An internet gateway is then established and configured to point to the VPC using MyAttachedGateway.

Included the skeleton of the three tier architecture. Unfortunately the skeleton was as far as I had gotten. For the static webnsite I created the S3 Bucket and manually uploaded the index.html to the bucket. For security reasons, and as best practices, the bucket blocks all public access. To allow for the content to be accessible I established a Cloud Front Distribution and configured it be the only source or Origin that the S3 bucket will accept requests from. I was able to successfully deply the stack using template.yaml. It produces the output for the site url. The current site url is https://d3r4qtkdk22u9h.cloudfront.net. The bucket itself is inaccessible and when attempting to access the bucket itself a "Access Denied" prompt is shown. For this I largely followed the available documentation found on Amazons Documentation site. 
https://docs.aws.amazon.com/pdfs/AmazonCloudFront/latest/DeveloperGuide/AmazonCloudFront\_DevGuide.pdf, https://docs.aws.amazon.com/pdfs/AWSCloudFormation/latest/APIReference/cfn-api.pdf, https://docs.aws.amazon.com/pdfs/AWSCloudFormation/latest/UserGuide/cfn-ug.pdf, https://docs.aws.amazon.com/pdfs/cloudformation-cli/latest/userguide/cloudformation-cli.pdf, https://docs.aws.amazon.com/pdfs/cloudfront/latest/APIReference/cloudfront-api.pdf

The three tier architecture with redundancy was a more difficult task. I got the majority of my ideas at the following link: https://repost.aws/articles/ARGpERJ3jISbOAlnmfVUsvMQ/building-a-secure-and-scalable-three-tier-architecture-on-aws-using-cloudformation and used several Claude prompts to provide me with an idea of the skeleton of the application

"I've been given an assignment for my CloudFormations class to create a static website hosted within an S3 Bucket. This was okay and I managed to get the webpage to be accessible. The second part of the assignment is to host a website and to 'Have a second set up for a 3 tier architecture for a web tier, application tier and 
database tier.'. I've found the following guide https://repost.aws/articles/ARGpERJ3jISbOAlnmfVUsvMQ/building-a-secure-and-scalable-three-tier-architecture-on-aws-using-cloudformation. Could you first provide in simple terms why the selected architecture has been choosen? Provide a list of the baseline required resources that needs to be established and why they are chosen."

I will provide the response in a file titled "LLM resposne" with the commit that makes these README updates.