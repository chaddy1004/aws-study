# Hello World

This goes through the "Hello World" using Serverless and AWS.

## Setup:
- Install [NodeJS](https://nodejs.org/en/download/)
- For serverless, install serverless by using the bash command:``` sudo npm install -g serverless```
- Install [aws-cli](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-mac.html)

## Creating IAM user for console:
- Follow [this guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html#id_users_create_console).
- Add the user to aws profile.
  - You do this by searching for IAM service by:
    - Service -> Search for "IAM" -> Add User
      - You can just use the default settings for this exercise
    - ```aws configure --profile <profile_name>```
        - https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html
        - For this exercise, the profile_name was set as "serverless"
        - ex) ```aws configre --profile serverless```

## Configuring Serverless:
- If the credential was not saved under a named_profile:
    - ```serverless config credentials --provider aws --key <ACCESS KEY ID> --secret <SECRET KEY>```
- With a named_profile:
    - ```serverless deploy --aws-profile <profile_name>```

## Initializing Project:
- Move to the directory, and call:
    - ```serverless create --template aws-python3 --name <service_name>```
        - This creates config.yml as well as the associated handler.py (This will also create gitgnore that ignores most of the boiler plate file directories

## Adding Events to our Function:
- Currently, there is no way to trigger the default function that is in handler
- You can add events like this:
```functions:
  hello:
    handler: handler.hello
    events:
      - http:
          path: hello-url
          method: get
```
- **Without the above, there is no endpoint url for us to see anything**

## Deploying the code to serverless:
- The directory that has handler.py and config.yml is a Serverless Service directory. Once in there, you can deploy the service by calling “serverless deploy”
    - https://www.serverless.com/framework/docs/providers/aws/cli-reference/deploy/
- To run with specific profile, there are few ways to specify it:
    - ```export AWS_PROFILE=“profile_name” && export AWS_REGION=“region_name”```
    - ```serverless deploy —aws-profile “profile_name”```
- For more details, check out this [guide](https://www.serverless.com/framework/docs/providers/aws/guide/credentials/)
- Once this is ran, you should be able to see an url in the deploy message 
    - Blahblahblah/“url_name”


## Removing Function
- Use “serverless remove” command to remove deployed service from AWS Lambda
