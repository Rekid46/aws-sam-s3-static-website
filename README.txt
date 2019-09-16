=> create below bucket to store artifacts when deployed through SAM
aws s3 mb s3://static-website-608965-artifacts --region=us-east-2

=> build the application
sam build

=> package the application
sam package --output-template-file packaged.yaml --s3-bucket static-website-608965-artifacts

=> deploy the application
sam deploy --template-file packaged.yaml --stack-name static-website-608965 --capabilities CAPABILITY_IAM --region us-east-2

=> copy index.html file into s3 bucket
aws s3 cp index.html s3://static-website-608965 --acl public-read