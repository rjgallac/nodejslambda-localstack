
aws --endpoint-url=http://localhost:4566 --region=us-east-1 iam create-role --role-name lambda-role --assume-role-policy-document file://role.json

aws --endpoint-url=http://localhost:4566 --region=us-east-1 lambda create-function --function-name work --zip-file fileb://index.zip --handler index.handler --runtime nodejs12.x --role arn:aws:iam::000000000000:role/lambda-role


aws --endpoint-url=http://localhost:4566 --region=us-east-1 lambda invoke --function-name work outputfile.txt

aws  --endpoint-url=http://localhost:4566 --region=us-east-1 lambda delete-function --function-name work


aws --endpoint-url=http://localhost:4566 --region=us-east-1 lambda list-functions



aws --endpoint-url=http://localhost:4566 --region=us-east-1 apigateway create-rest-api --name my-gateway

get the parent id
aws --endpoint-url=http://localhost:4566 --region us-east-1  apigateway get-resources --rest-api-id 2kj5nkbsjl 


aws --endpoint-url=http://localhost:4566 --region=us-east-1 apigateway create-resource \
    --rest-api-id 2kj5nkbsjl --parent-id hlx3kvqls9 --path-part "testwork"

aws apigateway put-method \
 --region us-east-1 \
 --rest-api-id 2kj5nkbsjl \
 --resource-id m1pvuditqy \
 --http-method GET \
 --authorization-type "NONE" \
--endpoint-url=http://localhost:4566

aws apigateway put-integration \
 --region us-east-1 \
 --rest-api-id 2kj5nkbsjl \
 --resource-id m1pvuditqy \
 --http-method GET \
 --type AWS_PROXY \
 --integration-http-method GET \
 --uri arn:aws:apigateway:us-east-1:lambda:path/2015-03-31/functions/arn:aws:lambda:us-east-1:000000000000:function:work/invocations \
 --passthrough-behavior WHEN_NO_MATCH \
 --endpoint-url=http://localhost:4566

 aws apigateway create-deployment \
 --region us-east-1 \
 --rest-api-id 2kj5nkbsjl \
 --stage-name test \
 --endpoint-url=http://localhost:4566

 http://localhost:4566/restapis/2kj5nkbsjl/test/_user_request_/test-work

aws  --region us-east-1 --endpoint-url=http://localhost:4566 apigateway get-rest-apis
aws --region us-east-1 --endpoint-url=http://localhost:4566 apigateway get-resources --rest-api-id m92mc7i0xp 
aws --region us-east-1 --endpoint-url=http://localhost:4566 apigateway delete-resource --resource-id k0hfgeaf5f  --rest-api-id m92mc7i0xp


DELETE API GATEWAY
aws --endpoint-url=http://localhost:4566 --region=us-east-1 apigateway delete-rest-api --rest-api-id 