# Amazon Rekognition identity\-based policy examples<a name="security_iam_id-based-policy-examples"></a>

By default, IAM users and roles don't have permission to create or modify Amazon Rekognition resources\. They also can't perform tasks using the AWS Management Console, AWS CLI, or AWS API\. An IAM administrator must create IAM policies that grant users and roles permission to perform specific API operations on the specified resources they need\. The administrator must then attach those policies to the IAM users or groups that require those permissions\.

To learn how to create an IAM identity\-based policy using these example JSON policy documents, see [Creating Policies on the JSON Tab](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create.html#access_policies_create-json-editor) in the *IAM User Guide*\.

**Topics**
+ [Policy best practices](#security_iam_service-with-iam-policy-best-practices)
+ [Using the Amazon Rekognition console](#security_iam_id-based-policy-examples-console)
+ [Example Amazon Rekognition Custom Labels policies](#security_iam_id-based-policy-examples-custom-labels)
+ [Example 1: Allow a user read\-only access to resources](#security_iam_id-based-policy-examples-read-only)
+ [Example 2: Allow a user full access to resources](#security_iam_id-based-policy-examples-full-acess)
+ [Allow users to view their own permissions](#security_iam_id-based-policy-examples-view-own-permissions)

## Policy best practices<a name="security_iam_service-with-iam-policy-best-practices"></a>

Identity\-based policies are very powerful\. They determine whether someone can create, access, or delete Amazon Rekognition resources in your account\. These actions can incur costs for your AWS account\. When you create or edit identity\-based policies, follow these guidelines and recommendations:
+ **Get started using AWS managed policies** – To start using Amazon Rekognition quickly, use AWS managed policies to give your employees the permissions they need\. These policies are already available in your account and are maintained and updated by AWS\. For more information, see [Get started using permissions with AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#bp-use-aws-defined-policies) in the *IAM User Guide*\.
+ **Grant least privilege** – When you create custom policies, grant only the permissions required to perform a task\. Start with a minimum set of permissions and grant additional permissions as necessary\. Doing so is more secure than starting with permissions that are too lenient and then trying to tighten them later\. For more information, see [Grant least privilege](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege) in the *IAM User Guide*\.
+ **Enable MFA for sensitive operations** – For extra security, require IAM users to use multi\-factor authentication \(MFA\) to access sensitive resources or API operations\. For more information, see [Using multi\-factor authentication \(MFA\) in AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html) in the *IAM User Guide*\.
+ **Use policy conditions for extra security** – To the extent that it's practical, define the conditions under which your identity\-based policies allow access to a resource\. For example, you can write conditions to specify a range of allowable IP addresses that a request must come from\. You can also write conditions to allow requests only within a specified date or time range, or to require the use of SSL or MFA\. For more information, see [IAM JSON policy elements: Condition](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition.html) in the *IAM User Guide*\.

## Using the Amazon Rekognition console<a name="security_iam_id-based-policy-examples-console"></a>

With the exception of the Amazon Rekognition Custom Labels feature, Amazon Rekognition doesn't require any addition permissions when using the Amazon Rekognition console\. For information about Amazon Rekognition Custom Labels, see [Step 5: Set Up Amazon Rekognition Custom Labels Console Permissions](https://docs.aws.amazon.com/rekognition/latest/dg/su-console-policy.html)\. 

You don't need to allow minimum console permissions for users that are making calls only to the AWS CLI or the AWS API\. Instead, allow access to only the actions that match the API operation that you're trying to perform\.

## Example Amazon Rekognition Custom Labels policies<a name="security_iam_id-based-policy-examples-custom-labels"></a>

You can create identity\-based policies for Amazon Rekognition Custom Labels\. For more information, see [Security](https://docs.aws.amazon.com/rekognition/latest/customlabels-dg/sc-introduction.html)\. 

## Example 1: Allow a user read\-only access to resources<a name="security_iam_id-based-policy-examples-read-only"></a>

The following example grants read\-only access to Amazon Rekognition resources\. 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "rekognition:CompareFaces",
                "rekognition:DetectFaces",
                "rekognition:DetectLabels",
                "rekognition:ListCollections",
                "rekognition:ListFaces",
                "rekognition:SearchFaces",
                "rekognition:SearchFacesByImage",
                "rekognition:DetectText", 
                "rekognition:GetCelebrityInfo",
                "rekognition:RecognizeCelebrities",
                "rekognition:DetectModerationLabels",  
                "rekognition:GetLabelDetection",
                "rekognition:GetFaceDetection",
                "rekognition:GetContentModeration",
                "rekognition:GetPersonTracking",
                "rekognition:GetCelebrityRecognition",
                "rekognition:GetFaceSearch",
                "rekognition:GetTextDetection",
                "rekognition:GetSegmentDetection",
                "rekognition:DescribeStreamProcessor",
                "rekognition:ListStreamProcessors",
                "rekognition:DescribeProjects",
                "rekognition:DescribeProjectVersions",
                "rekognition:DetectCustomLabels",
                "rekognition:DetectProtectiveEquipment",
                "rekognition:ListTagsForResource",
               "rekognition:ListDatasetEntries",
                "rekognition:ListDatasetLabels",
                "rekognition:DescribeDataset"

            ],
            "Resource": "*"
        }
    ]
}
```

## Example 2: Allow a user full access to resources<a name="security_iam_id-based-policy-examples-full-acess"></a>

The following example grants full access to Amazon Rekognition resources\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "rekognition:*"
            ],
            "Resource": "*"
        }
    ]
}
```

## Allow users to view their own permissions<a name="security_iam_id-based-policy-examples-view-own-permissions"></a>

This example shows how you might create a policy that allows IAM users to view the inline and managed policies that are attached to their user identity\. This policy includes permissions to complete this action on the console or programmatically using the AWS CLI or AWS API\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "ViewOwnUserInfo",
            "Effect": "Allow",
            "Action": [
                "iam:GetUserPolicy",
                "iam:ListGroupsForUser",
                "iam:ListAttachedUserPolicies",
                "iam:ListUserPolicies",
                "iam:GetUser"
            ],
            "Resource": ["arn:aws:iam::*:user/${aws:username}"]
        },
        {
            "Sid": "NavigateInConsole",
            "Effect": "Allow",
            "Action": [
                "iam:GetGroupPolicy",
                "iam:GetPolicyVersion",
                "iam:GetPolicy",
                "iam:ListAttachedGroupPolicies",
                "iam:ListGroupPolicies",
                "iam:ListPolicyVersions",
                "iam:ListPolicies",
                "iam:ListUsers"
            ],
            "Resource": "*"
        }
    ]
}
```