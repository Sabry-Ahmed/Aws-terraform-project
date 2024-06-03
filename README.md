# Terraform AWS Infrastructure Project

This project contains Terraform configurations to provision AWS resources, including an S3 bucket, an EC2 instance, and a DynamoDB table.

## Prerequisites

- [Terraform](https://www.terraform.io/downloads.html) v1.2.0 or higher
- AWS account credentials

## AWS Resources Provisioned

1. **S3 Bucket**
   - Name: `myfirstbucketsszaqs`
   - Tags:
     - Name: `My bucket`

2. **EC2 Instance**
   - AMI: `ami-0c7217cdde317cfec`
   - Instance Type: `t2.micro`
   - Tags:
     - Name: `ExampleAppServerInstance`

3. **DynamoDB Table**
   - Name: `FirstTab`
   - Billing Mode: `PROVISIONED`
   - Read Capacity: 20
   - Write Capacity: 20
   - Attributes:
     - Hash Key: `UserId` (String)
     - Range Key: `GameTitle` (String)
     - Additional Attribute: `TopScore` (Number)
   - TTL:
     - Attribute Name: `TimeToExist`
     - Enabled: `false`
   - Global Secondary Index:
     - Name: `GameTitleIndex`
     - Hash Key: `GameTitle`
     - Range Key: `TopScore`
     - Write Capacity: 10
     - Read Capacity: 10
     - Projection Type: `INCLUDE`
     - Non-Key Attributes: `UserId`
   - Tags:
     - Name: `dynamodb-table-1`
     - Environment: `production`

## Usage

1. **Clone the repository**

   ```sh
   git clone <repository-url>
   cd <repository-directory>
   ```

2. **Initialize Terraform**

   ```sh
   terraform init
   ```

3. **Apply the Terraform configuration**

   ```sh
   terraform apply
   ```

   Confirm the apply step with `yes`.

4. **Destroy the Terraform-managed infrastructure (when no longer needed)**

   ```sh
   terraform destroy
   ```

   Confirm the destroy step with `yes`.

## AWS Credentials

Ensure your AWS credentials are set in your environment. For example:

```sh
export AWS_ACCESS_KEY_ID="your_access_key_id"
export AWS_SECRET_ACCESS_KEY="your_secret_access_key"
```

Or configure the provider directly in the `main.tf` (as done in this project):

```hcl
provider "aws" {
   region      = "us-east-1"
   access_key  = "your_access_key_id"
   secret_key  = "your_secret_access_key"
}
```

## Notes

- Replace `<repository-url>` and `<repository-directory>` with your repository details.
- Ensure your AWS credentials are kept secure and never hardcoded in your source files.

