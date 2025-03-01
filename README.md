# AWS Security Reference Architecture Examples<!-- omit in toc -->

Copyright Amazon.com, Inc. or its affiliates. All Rights Reserved. SPDX-License-Identifier: CC-BY-SA-4.0

## Table of Contents<!-- omit in toc -->

- [Introduction](#introduction)
- [Example Solutions](#example-solutions)
- [Utils](#utils)
- [Repository and Solution Naming Convention](#repository-and-solution-naming-convention)
- [Frequently Asked Questions](#frequently-asked-questions)
- [Contributors](#contributors)
- [License Summary](#license-summary)

## Introduction

This repository contains AWS CloudFormation templates to help developers and engineers deploy AWS security-related services in a multi-account environment following patterns that align with the
[AWS Security Reference Architecture](https://docs.aws.amazon.com/prescriptive-guidance/latest/security-reference-architecture/). The Amazon Web Services (AWS) Security Reference Architecture (AWS SRA) is a holistic set of guidelines for deploying
the full complement of AWS security services in a multi-account environment.

The AWS service configurations and resources (e.g. IAM roles and policies) deployed by these templates are deliberately very restrictive. They are intended to illustrate an implementation path rather than provide a complete solution. You will need to
modify and tailor these templates to suit your individual environment and security needs.

The examples within this repository have been deployed and tested using the corresponding deployment platform (e.g. AWS Control Tower and AWS CloudFormation StackSets).

## Example Solutions

- CloudTrail
  - [Organization CloudTrail](aws_sra_examples/solutions/cloudtrail/cloudtrail_org)
- Config
  - [Organization Aggregator](aws_sra_examples/solutions/config/config_aggregator_org)
  - [Organization Conformance Pack](aws_sra_examples/solutions/config/config_conformance_pack_org)
- EC2
  - [EC2 Default EBS Encryption](aws_sra_examples/solutions/ec2/ec2_default_ebs_encryption)
- Firewall Manager
  - [Organization Firewall Manager](aws_sra_examples/solutions/firewall_manager/firewall_manager_org)
- GuardDuty
  - [Organization GuardDuty](aws_sra_examples/solutions/guardduty/guardduty_org)
- IAM
  - [Access Analyzer](aws_sra_examples/solutions/iam/iam_access_analyzer)
  - [Account Password Policy](aws_sra_examples/solutions/iam/iam_password_policy_acct)
- Macie
  - [Organization Macie](aws_sra_examples/solutions/macie/macie_org)
- S3
  - [S3 Block Account Public Access](aws_sra_examples/solutions/s3/s3_block_account_public_access)
- SecurityHub
  - [Account SecurityHub Enabler](aws_sra_examples/solutions/securityhub/securityhub_enabler_acct)

## Utils

- [Prerequisites for AWS Control Tower solutions](aws_sra_examples/utils/aws_control_tower/prerequisites)
- packaging_scripts
  - package-lambda.sh (Creates the Lambda zip file and uploads to an S3 bucket)

## Repository and Solution Naming Convention

The repository is organized by AWS service solutions, which include deployment platforms (e.g., AWS Control Tower and AWS CloudFormation StackSet).

**Example:**

```shell
.
├── solutions
│   ├── guardduty
│   │   └── guardduty_org
│   │       ├── README.md
│   │       ├── customizations_for_aws_control_tower
│   │       │   ├── manifest-v2.yaml
│   │       │   ├── manifest.yaml
│   │       │   └── parameters
│   │       ├── documentation
│   │       ├── lambda
│   │       │   └── src
│   │       │       ├── app.py
│   │       │       └── requirements.txt
│   │       └── templates
│   │           ├── guardduty-org-configuration-role.yaml
│   │           ├── guardduty-org-configuration.yaml
│   │           ├── guardduty-org-delete-detector-role.yaml
│   │           ├── guardduty-org-delivery-kms-key.yaml
│   │           └── guardduty-org-delivery-s3-bucket.yaml
│   ├── ...
```

The example solutions within this repository can be managed/deployed to accounts using AWS Organizations or directly within individual accounts. The suffix on the solution name identifies how the solution is managed/deployed.

| Solution Suffix | Description                                                         |
| --------------- | ------------------------------------------------------------------- |
| acct            | The solution is managed/deployed within each account                |
| org             | The solution is managed/deployed to accounts via AWS Organizations  |
| ou              | The solution is managed/deployed to accounts via Organization Units |

## Frequently Asked Questions

Q. How were these particular solutions chosen? A. All the examples in this repository are derived from common patterns that many customers ask us to help them deploy within their environments. We will be adding to the examples over time.

Q. How were these solutions created? A. We’ve collected, cataloged, and curated our multi-account security solution knowledge based on working with a variety of AWS customers.

Q. Who is the audience for these AWS Security Reference Architecture examples? A. Security professionals that are looking for illustrative examples of deploying security patterns in AWS. These code samples provide a starting point from which you can
build and tailor infrastructure for your needs.

Q. Why didn't the solutions use inline Lambda functions within the CloudFormation templates? A. Reasons:

- You should control the dependencies in your function's deployment package as stated in the [best practices for working with AWS Lambda functions](https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html).
- The [AWS Lambda runtimes](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html) might not be the latest version, which contains a feature that is needed for the solution.

Q. I have ideas to improve this repository. What should I do? A. Please create an issue or submit a pull request.

## Contributors

[Contributors](CONTRIBUTORS)

## License Summary

The documentation is made available under the Creative Commons Attribution-ShareAlike 4.0 International License. See the LICENSE file.

The sample code within this documentation is made available under the MIT-0 license. See the LICENSE-SAMPLECODE file.

Please note when building the project that some of the configured developer dependencies are subject to copyleft licenses. Please review these as needed for your use.
