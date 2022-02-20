# Maven terraform Buildkite Plugin

Automates maven build creation and load the build to cloud using terraform

## Example

sample `pipeline.yml`:

```yml
steps:
  - label: ":package: Deploy"
    plugins:
        - madan712/maven-terraform:
```

below is the sample .tf file to create AWS lambda function `main.tf`:

```yml
variable "build" {}

terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 3.27"
    }
  }

  required_version = ">= 0.14.9"
}

provider "aws" {
  profile = "default"
  region  = "us-east-1"
}

resource "aws_lambda_function" "aws_lambda_demo" {
  filename         = var.build
  function_name    = "awsLambdaDemo"
  role             = "arn:aws:iam::695663959248:role/lambda-role"
  handler          = "com.javaxp.lambda.demo.LambdaFunctionHandler::handleRequest"
  runtime          = "java11"
  source_code_hash = filebase64sha256(var.build)
}
```

## Configuration

### Not applicable

## Developing

To run the tests:

```
TODO
```

## Contributing

1. Fork the repo
2. Make the changes
3. Run the tests
4. Commit and push your changes
5. Send a pull request
