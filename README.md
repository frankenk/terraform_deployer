Simple python code to make terraform deploying easier in my other python projects. Uses Docker SDK for python to run and deploy Terraform code in current directory. 

Assumes that AWS s3 is used for terraform state file.

## Requirements

Uses Docker to run terraform in container. Also python docker sdk and boto3 libraries. 

Install by running `pip install -r requirements.txt`

## Usage

Import the code: `import terraform_deployer`

Run Terraform commands using following `run_terraform_command` function: `run_terraform_command(command, s3_state, region, vars=None)`
- `command` - main terraform commands (e.g. plan, ).
- `s3_state` - bucket name where state file resides.
- `region` - AWS region.
- `vars` - manually specify terraform variable values, see examples below.

```
run_terraform_command("plan", "tf-shodanmore-statefile-temp-2", "eu-west-1")

variables = {
    "bucket_tag_name": "can_be_deleted",
    "bucket_tag_env": "dev"
}
 
run_terraform_command(
    "apply -auto-approve", "tf-shodanmore-statefile-temp-2", "eu-west-1", variables
    )
```

Do not need to run terraform `init` as the code creates S3 bucket for state file if one does not exists and initiates terraform. 

 
