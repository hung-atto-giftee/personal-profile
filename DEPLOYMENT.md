# GitHub Actions S3 Deployment Setup

## Required GitHub Secrets

To use the S3 deployment action, you need to configure the following secrets in your GitHub repository:

### Required Secrets

1. **AWS_ACCESS_KEY_ID** - Your AWS access key ID
2. **AWS_SECRET_ACCESS_KEY** - Your AWS secret access key  
3. **AWS_REGION** - AWS region where your S3 bucket is located (e.g., `us-east-1`, `ap-southeast-1`)
4. **S3_BUCKET_NAME** - The name of your S3 bucket

### Optional Secrets

5. **CLOUDFRONT_DISTRIBUTION_ID** - CloudFront distribution ID (if you want to invalidate cache after deployment)

## How to Add Secrets

1. Go to your GitHub repository
2. Navigate to **Settings** → **Secrets and variables** → **Actions**
3. Click **New repository secret**
4. Add each secret with its corresponding value

## AWS IAM Policy

A complete IAM policy JSON file is provided in [`iam-policy.json`](iam-policy.json).

**Before using the policy:**
1. Replace `YOUR_BUCKET_NAME` with your actual S3 bucket name
2. Attach this policy to your IAM user or role

### How to apply the policy:

1. **Via AWS Console:**
   - Go to IAM → Users/Roles → Select your user/role
   - Click "Add permissions" → "Attach policies directly" 
   - Click "Create policy" → JSON tab → Paste the content from `iam-policy.json`
   - Remember to replace `YOUR_BUCKET_NAME` with your bucket name

2. **Via AWS CLI:**
   ```bash
   aws iam create-policy \
     --policy-name S3DeploymentPolicy \
     --policy-document file://iam-policy.json
   ```

## Trigger

The action will automatically run whenever you push commits to the `develop` branch.