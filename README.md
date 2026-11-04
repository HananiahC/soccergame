# Soccer Trivia

Daily soccer puzzles (Mystery Player, Career Path and more) on a serverless AWS backend.

## Architecture (so far)
- **Website:** private S3 bucket served only through CloudFront (Origin Access Control), HTTPS, AWS managed security headers
- **Infrastructure:** Terraform, with remote state in an encrypted, versioned S3 bucket using native S3 state locking

Coming next: Lambda + API Gateway + DynamoDB, the GitHub Actions DevSecOps pipeline, load testing, and an AI hint assistant on Amazon Bedrock.

## Deploy
```bash
# One time: create the Terraform state bucket
cd infra/bootstrap && terraform init && terraform apply

# The website
cd ../site
cp backend.hcl.example backend.hcl   # paste the bucket name from the step above
terraform init -backend-config=backend.hcl
terraform apply
```

## Tear down
```bash
cd infra/site && terraform destroy
```
