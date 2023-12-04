# Imposter Mock API github action

A test repository to generate imposter configuration file from an openapi specification file.

The following github environment variables and secrets need to be set:

- Secrets
  - `AWS_ACCESS_KEY_ID` : The access key id for the AWS account. You can find these value in AWS Parameter Store with the name `/dev/stub-api/infra/cicd_user_access_key`.
  - `AWS_SECRET_ACCESS_KEY` : The access key secret for the AWS account. You can find these value in AWS Parameter Store with the name `/dev/stub-api/infra/cicd_user_secret_key`.

When launching the workflow, you will be prompted to fill in the following inputs:

- `project_name` : The name of the project for which you are deploying a stub api. This will be used for the path of the s3 folder and stub api endpoint.
- `stub_api_name` : The name of the stub api. This will be used for the path of the s3 folder and stub api endpoint.
- `openapi_file_path` : Path of the OpenAPI specification file.

This workflow will do the following:

- Automatically generate the configuration file for the Imposter lambda function to run from the OpenAPI specification file.
- Upload the configuration file for the Imposter lambda function in the S3 bucket.
- Force refresh the lambda function to make the new endpoints available.

The stub api should be available on the following URL:

```(sh)
https://lambda-function-url/<project_name>/<stub_api_name>/<endpoint>
```
