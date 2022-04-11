# Terraform code generation from Duplo Tenant

## Prerequisite

1. Terraform version greater than or equals to `v0.14.11`
2. Create named profiles for the AWS CLI, [Refer](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html)
   Lets say `duplo-msp` aws profile is created.
3. Following environment variables to be exported in the shell while running this projects.

```shell
# Required Vars
export customer_name="duplo-masp"
export tenant_id="7d1b0f7e-fcc0-4118-ad5a-b448bf0eac41"
export cert_arn="arn:aws:acm:us-west-2:128329325849:certificate/1234567890-aaaa-bbbb-ccc-66e7dcd609e1"
export duplo_host="https://msp.duplocloud.net"
export duplo_token="xxx-xxxxx-xxxxxxxx"
export aws_account_id="128329325849"
# Optional Vars
export duplo_provider_version="0.7.0"
export tenant_project="admin-tenant"
export aws_services_project="aws-services"
export app_project="app"
export generate_tf_state="false" # if true, State files will be generated
export s3_backend="false" # if true, State files are stored in s3 bucket named "duplo-tfstate-<account-id>"

# Needed for S3 backend
export AWS_ACCESS_KEY_ID="xxx-xxxxx-xxxxxxxx"
export AWS_SECRET_ACCESS_KEY="xxx-xxxxx-xxxxxxxx"
export AWS_DEFAULT_REGION="us-west-2"
#Or
export AWS_PROFILE="duplo-msp"
```

4. S3 Bucket for terraform remote state which is created by duplo automatically with the name `duplo-tfstate-128329325849`

   

## How to run ?

- Clone this repository.

- Prepare environment variables as mentioned above.

- Run using  following command

  ```shell
  make run
  ```

- **Output** : target folder is created along with customer name as mention in env vars. This will contain all terraform projects as mentioned below.

  - **Project : admin-tenant** This projects manages creation of duplo tenant.
  - **Project : aws-services** This project manages data services like Redis, RDS, Kafka, S3 buckets, Elastic Search inside duplo.
  - **Project : app** This project manages duplo services like eks and ecs etc.

