# aws-certbot

A Slack bot for recording AWS certifications you've earned.

## Pre-reqs

- You've deployed this service successfully (see https://github.com/pariveda-serverless/support/tree/master/create-new-service)
- Get the API Gateway URL. You'll use it at the 'Request URL' configuration step:

    ``` 
    $ aws cloudformation describe-stacks --stack-name aws-certbot-master --query 'Stacks[0].Outputs[?OutputKey==`ServiceEndpoint`].OutputValue' --output text
    
    Hint: stack-name is the service followed by a '-' then the stage/branch
    ``` 
    
- You have a Slack development workspace

- You've created a new app at https://api.slack.com/apps?new_app=1 in that development workspace

- You've created a slash command at https://api.slack.com/apps/A9ZA995GF/slash-commands? (where 'A9ZA995GF' corresponds to the link for your development workspace)

- Enter The following values will work (append the function name to the API Gateway URL above):

    ``` 
    Command: /aws-cert
    Request URL: https://xvwjphbae3.execute-api.us-east-1.amazonaws.com/master/hello/world
    Short Description: Log and share the AWS certs you've worked so hard to earn
    Usage Hint: [Validation Number]
    ```
- At 'Oauth & Permissions' click 'Install App to Workspace' (https://api.slack.com/apps/A9ZA995GF/oauth?)

- Save the value in ~/secrets/oauth.txt
    
    ``` 
    echo -n "xoxp-xxxxxxxxx-xxxxxxx-yyyyyyy" > ~/secrets/oauth.txt
    ```
    
- Encrypt and upload the file (see https://github.com/pariveda-serverless/support/tree/master/secrets-uploader for more details)

    ``` 
    ~/src/support/secrets-uploader $ docker-compose run --rm secrets
    /var/aws $ ./upload.sh -service aws-certbot -stage master -path /var/secrets/oauth.txt -s3key oauth.enc
    ```
    
    If you see something like 'Done - file saved to: aws-certbot-security-master-secretsbucket-b39999jbnza8/oauth.enc!' you are good to move on.

- Follow the same process for uploading the 'Verification Token' at (the shared secret that tells your app the incoming request is really from Slack), naming the file 'token.txt'. 

  You'll find it at https://api.slack.com/apps/A9ZA995GF/general?
  
  ``` 
  echo -n "8xxxxxxxxxxxxxxxxxx" > ~/secrets/token.txt
  ~/src/support/secrets-uploader $ docker-compose run --rm secrets
  ./upload.sh -service aws-certbot -stage master -path /var/secrets/token.txt -s3key token.enc
  ```

- Add the following permissions at https://api.slack.com/apps/A9ZA995GF/oauth?

    ``` 
    Access user’s profile and workspace profile fields
    ------------------
    users.profile:read
    
    Access your workspace’s profile information
    ------------------
    users:read
    
    View email addresses of people on this workspace
    ------------------
    users:read.email
    
    Upload and modify files as user
    ------------------
    files:write:user
    ```

- Use  to upload the fo

## Contributing

1. Fork the repository
1. Add cool stuff
1. Submit a pull request
1. Get credit!


