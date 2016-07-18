
# Interacting with Amazon AWS using the CLI

## Installation

You need Python and pip.

$ pip install awscli

On my Mac (El Capitan) using a virtualenv:

$ /Users/kayeva/.virtualenvs/env-aws/bin/pip install awscli --ignore-installed six

$ /Users/kayeva/.virtualenvs/env-aws/bin/aws --version

$ aws-cli/1.10.38 Python/2.7.11 Darwin/15.5.0 botocore/1.4.28


## Configuration

$ aws configure
AWS Access Key ID [None]: AKIAIOSFODNN7EXAMPLE
AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
Default region name [None]: eu-central-1
Default output format [None]: json

The AWS CLI will prompt you for four pieces of information. AWS Access Key ID and AWS Secret Access Key are your account credentials. If you don't have keys, see the Getting Set Up section earlier in this guide.

Default region is the name of the region you want to make calls against by default. This is usually the region closest to you, but it can be any region.

The AWS CLI looks for credentials and configuration settings in the following order:

1/ Command Line Options – region, output format and profile can be specified as command options to override default settings.

2/ Environment Variables – AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, etc.

Environment variables override configuration and credential files and can be useful for scripting or temporarily setting a named profile as the default.

The following variables are supported by the AWS CLI

AWS_ACCESS_KEY_ID – AWS access key.

AWS_SECRET_ACCESS_KEY – AWS secret key. Access and secret key variables override credentials stored in credential and config files.

AWS_SESSION_TOKEN – session token. A session token is only required if you are using temporary security credentials.

AWS_DEFAULT_REGION – AWS region. This variable overrides the default region of the in-use profile, if set.

AWS_DEFAULT_PROFILE – name of the CLI profile to use. This can be the name of a profile stored in a credential or config file, or default to use the default profile.

AWS_CONFIG_FILE – path to a CLI config file.

### Notes regarding the AWS credentials file

Located at ~/.aws/credentials. This file can contain multiple named profiles in addition to a default profile.

TODO...

### Notes regarding the AWS CLI configuration file

Typically located at ~/.aws/config...

TODO...


## Usage

Checking your resources in multiple regions and changing output format 
for legibility or ease of use when scripting. 

$ aws ec2 describe-instances --output table --region us-east-1

$ aws ec2 describe-instances --output table --region us-west-1

TODO...
