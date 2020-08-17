## Defense In Depth using AWS Managed Rules - Blog Post

This repo holds supporting documentation for the AWS Security Blog post deploying a multi-layered Web ACL on AWS WAF using AWS CloudFormation templates. This helps customers get started with AWS Managed Rules and implement their security enforcement based on the same development best practices they are used to.

These AWS CloudFormation does not create the required Amazon CloudFront or Application Load Balancers. They are only for creating Web ACL's for these resources while using AWS Managed Rules in doing so.

You will find that there are four CloudFormation templates. 


## CloudFormation Template Overview 

"Amazon-CloudFront-Application-Load-Balancer-AMR.yml" ->
Creates a single stack in us-east-1 that deploys two web ACL’s. One for the CloudFront distribution that enforces rate-limits on HTTP GET and POST requests to mitigate against HTTP floods. In this web ACL it also makes use of the AWS Managed Rule Sets which includes AWSManagedRulesAmazonIpReputationList, AWSManagedRulesCommonRuleSet, AWSManagedRulesKnownBadInputsRuleSet and AWSManagedRulesAdminProtectionRuleSet as part of the edge network policy enforcement. The second web ACL is created also in us-east-1, but this is a regional web ACL to protect the CloudFront distribution’s origin Load Balancer from known application layer attacks using Amazon Managed Rule Sets. Such as AWSManagedRulesSQLiRuleSet, AWSManagedRulesLinuxRuleSet, AWSManagedRulesUnixRuleSet, AWSManagedRulesPHPRuleSet and AWSManagedRulesWordPressRuleSet.

"Amazon-CloudFront-EdgeLayer-AMR.yml" ->
Creates a single stack in us-east-1 that deploys one web ACL for the CloudFront distribution that enforces rate-limits on HTTP GET and POST requests to mitigate against HTTP floods. In this web ACL it also makes use of the AWS Managed Rule Sets which includes AWSManagedRulesAmazonIpReputationList, AWSManagedRulesCommonRuleSet, AWSManagedRulesKnownBadInputsRuleSet and AWSManagedRulesAdminProtectionRuleSet as part of the edge network policy enforcement.

"ApplicationLayer-Load-Balancer-AMR.yml" ->
Creates a single stack in the region of the Load Balancer that creates one web ACL. This is a regional web ACL to protect the CloudFront distribution’s origin Load Balancer from known application layer attacks using Amazon Managed Rule Sets. Such as AWSManagedRulesSQLiRuleSet, AWSManagedRulesLinuxRuleSet, AWSManagedRulesUnixRuleSet, AWSManagedRulesPHPRuleSet and AWSManagedRulesWordPressRuleSet.

"EdgeLayerALB-PrivateLayerALB-AMR.yml" ->
Creates a single stack in the region of the Load Balancer that creates two web ACL’s. One would be for the public facing Load Balancer that will enforce rate-limits on HTTP GET and POST requests to mitigate against HTTP floods. It will also make use of AWS Managed Rule Sets which includes AWSManagedRulesAmazonIpReputationList, AWSManagedRulesCommonRuleSet, AWSManagedRulesKnownBadInputsRuleSet and AWSManagedRulesAdminProtectionRuleSet as part of the edge network policy enforcement. The second web ACL is created also the same region, but it is for a private Load Balancer to protect it from known application layer attacks using Amazon Managed Rule Sets. Such as AWSManagedRulesSQLiRuleSet, AWSManagedRulesLinuxRuleSet, AWSManagedRulesUnixRuleSet, AWSManagedRulesPHPRuleSet and AWSManagedRulesWordPressRuleSet.



## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## Extra Documentation
https://d1.awsstatic.com/whitepapers/guidelines-implementing-aws-waf.pdf 

## License

This library is licensed under the MIT-0 License. See the LICENSE file.

