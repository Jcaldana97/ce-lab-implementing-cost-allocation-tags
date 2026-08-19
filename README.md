# Lab M7.02 - Implementing Cost Allocation Tags

## Design Tag Taxonomy

Definition of required tags, naming conventions and enforcement can be found in *tagging-strategy.md* file. 

## Tagging Resources

Using AWS Tag Editor:

1. AWS Console → Resource Groups → Tag Editor

2. Find resources:

    - Region: All regions
    - Resource types: EC2 instance, S3 bucket, RDS database

3. Search

4. Select resources (at least 10)

5. Manage tags → Add:

    - Environment: development (or appropriate value)
    - Owner: your-name
    - Project: bootcamp
    - CostCenter: training

6. Review and apply tags

AWS CLI Command (alternative):

```bash
aws ec2 create-tags \
  --resources i-1234567890abcdef0 \
  --tags Key=Environment,Value=development \
         Key=Owner,Value=platform-team \
         Key=Project,Value=web-app \
         Key=CostCenter,Value=eng-001
```

## Activate Cost Allocation Tags

1. Billing Console → Cost Allocation Tags
2. Find your tags in "User-defined cost allocation tags"
3. Select: Environment, Owner, Project, CostCenter
4. Activate tags

## View Costs by Tags

In Cost Explorer

- Group by: Tag → Environment
- View production vs development vs staging costs

![Cost by Environment](screenshots/costs-by-environment.png)

In another view:

- Group by: Tag → Owner
- Costs per team/owner

![Cost by Owner](screenshots/costs-by-owner.png)

## Set Up AWS Config Rule

Create Config rule for required tags:

1. AWS Config → Rules → Add rule

2. Search "required-tags"

3. Configure:

    - tag1Key: Environment
    - tag2Key: Owner
    - tag3Key: Project
    - tag4Key: CostCenter

4. Choose resource types: EC2, S3

5. Create rule

![Compliance](screenshots/config-compliance.png)