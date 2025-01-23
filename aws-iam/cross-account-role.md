# Create a role in the target account

1. Select 'another account' as the trusted entity
2. Enter the account ID and check the 'Require external ID' checkbox
3. Enter the external ID
4. Attach the following policy to the role:

{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowBucketAccess",
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:PutObject",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::<bucket-name>",
                "arn:aws:s3:::<bucket-name>/*"
            ]
        }
    ]
}

# Assume the role in the target account

1. Run the following command to assume the role using the CLI

aws sts assume-role --role-arn arn:aws:iam::692859928929:role/Cross-account-test --role-session-name mysession --external-id PASS123456

2. Configure the credentials
3.     

aws configure set aws_access_key_id <> --profile target-account
aws configure set aws_secret_access_key <> --profile target-account
aws configure set aws_session_token <> --profile target-account

3. Run CLI commands against the bucket

aws s3 ls s3://test-cross-account-s3214 --profile target-account
