# Static Website Deployment

Github action for deploying a static website to AWS S3 and invalidate CloudFront distribution

## Usage

Example workflow file:

```yaml
name: Deploy

on:
  push:
    branches:
      - master
    
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    permissions:
      id-token: write
      contents: read

    steps:
      - name: Check out repository
        uses: actions/checkout@v3

      - name: Deploy to S3
        uses: lukeharback/s3-cloudfront-deploy@v1.0.0
        with:
          folder: src
          aws-ami-role: ${{ secrets.AWS_AMI_ROLE }}
          aws-region: ${{ secrets.AWS_REGION }}
          aws-bucket: ${{ secrets.AWS_BUCKET }}
          aws-distribution-id: ${{ secrets.DISTRIBUTION_ID }}
          aws-invalidation-path: '/*'
```

## Configuration

| Name | Description | Required |
| --- | --- | --- | 
| folder | Build folder to deploy | Yes | 
| aws-ami-role | AWS IAM Role | Yes | 
| aws-region | AWS Region (eg. ap-southeast-2) | Yes | 
| aws-bucket | Name of AWS S3 Bucket | Yes | 
| aws-distribution-id | AWS CloudFront Distribution ID | Yes | 
| aws-invalidation-path | AWS CloudFront Invalidation Path (eg. '/*' ) | Yes | 

