# Imposter Mock API github action

A test repository to generate imposter configuration file from an openapi specification file.

The following github environment variables and secrets need to be set:

- Secrets
  - `AWS_ACCESS_KEY_ID` : The access key id for the AWS account
  - `AWS_SECRET_ACCESS_KEY` : The access key secret for the AWS account
  - `S3_BUCKET` : S3 Bucket for the Imposter stub api
- Environment variable
  - `AWS_DEFAULT_REGION` : The region for the AWS account
  - `LAMBDA_FUNCTION_NAME` : The Imposter lambda function name

When launching the workflow, you will be prompted to fill in the following inputs:

- `project_name` : The name of the project for which you are deploying a stub api. This will be used for the path of the s3 folder and stub api endpoint.
- `stub_api_name` : The name of the stub api. This will be used for the path of the s3 folder and stub api endpoint.
- `openapi_file_path` : Path of the OpenAPI specification file.

The github action will do the following:

- Automatically generate the configuration file for the Imposter lambda function to run from the OpenAPI specification file.
- Upload the configuration file for the Imposter lambda function in the S3 bucket.
- Force refresh the lambda function to make the new endpoints available.

The stub api should be available on the following URL:

```(sh)
https://lambda-function-url/<project_name>/<stub_api_name>/<endpoint>
```
