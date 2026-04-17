# Question

As part of a data migration project, the team lead has tasked the team with migrating data from an existing S3 bucket to a new S3 bucket. The existing bucket contains a substantial amount of data that must be accurately transferred to the new bucket. The team is responsible for creating the new S3 bucket and ensuring that all data from the existing bucket is copied or synced to the new bucket completely and accurately. It is imperative to perform thorough verification steps to confirm that all data has been successfully transferred to the new bucket without any loss or corruption.
As a member of the Nautilus DevOps Team, your task is to perform the following:

Create a New Private S3 Bucket: Name the bucket devops-sync-21322.
Data Migration: Migrate the entire data from the existing devops-s3-2666 bucket to the new devops-sync-21322 bucket.
Ensure Data Consistency: Ensure that both buckets have the same data.
Use AWS CLI: Use the AWS CLI to perform the creation and data migration tasks.

# Solution

```
# Step 1: Check existing bucket
aws s3 ls
aws s3 ls s3://devops-s3-2666 --recursive --summarize

# Step 2: Create new private bucket
aws s3 mb s3://devops-sync-21322

# Step 3: Ensure bucket is private
aws s3api put-public-access-block \
  --bucket devops-sync-21322 \
  --public-access-block-configuration \
  BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=true,RestrictPublicBuckets=true

# Step 4: Sync data
aws s3 sync s3://devops-s3-2666 s3://devops-sync-21322

# Step 5: Verify - compare counts
aws s3 ls s3://devops-s3-2666 --recursive --summarize
aws s3 ls s3://devops-sync-21322 --recursive --summarize

# Step 6: Verify - dry run (should show nothing)
aws s3 sync s3://devops-s3-2666 s3://devops-sync-21322 --dryrun
```

