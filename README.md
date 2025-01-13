#### Set up DEV in your account
1. `ln -s ../driver-frontend driver-frontend` # create link to frontend directory
2. `aws configure --profile ps_dev` # configure your DEV aws profile
3. `asp ps_dev` # activate 
4. `export CDK_DOMAIN_NAME=prettysolution.com` # set hosted zone, must exist in route53 in your ps_dev account
5. `npx projen cdk:dev ls` # list stacks
6. `npx projen cdk:dev deploy local-pipeline/local/ApiGatewayStack -e` # deploy stack

#### run express in server mode
1. follow steps from [Set up DEV in your account](#set-up-dev-in-your-account)
2. export REPORT_TABLE_NAME=$(aws ssm get-parameter --name "/core/DynamoDbStack/Tables/Report" --query "Parameter.Value" --output text)
3. nodemon src/stacks/api/report/server.ts
4. [test your api](src/stacks/api/report/debug/report-api.http)