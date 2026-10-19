# AWS Cloud Security Investigation & Risk Assessment

## Project Overview
Conducted a hands-on AWS cloud security assessment to evaluate Amazon S3 access controls, encryption settings, IAM configurations, and CloudTrail audit logging. The project focused on identifying security risks, verifying existing protections, and recommending improvements based on observed evidence.

## Objectives
- Evaluate Amazon S3 public access controls.
- Verify server-side encryption for stored objects.
- Review AWS IAM users, roles, and permissions.
- Investigate AWS CloudTrail management events.
- Document security findings and risk mitigation recommendations.

## AWS Services Examined
- **Amazon S3:** Object storage, encryption, and access control
- **AWS IAM:** Identity and access management
- **AWS CloudTrail:** Management-event auditing

## Methodology

### 1. S3 Security Assessment
Created a test bucket named `oak-cloud-security-lab-2026` in the `us-east-2` region.

Reviewed the following configurations:
- S3 Block Public Access enabled
- Bucket owner enforced, with ACLs disabled
- Default server-side encryption using Amazon S3 managed keys (SSE-S3)
- No bucket policy configured

Uploaded a harmless text file named `security-test.txt` and verified its object-level encryption.

### 2. Anonymous Access Test
Copied the test object's URL and attempted to access it from an unauthenticated browser session.

**Result:** The request returned `AccessDenied`.

This demonstrated that anonymous read access to the tested object was denied. The test does not establish that every object or access path is protected.

### 3. IAM Security Review
Reviewed the AWS account's IAM configuration.

Observations:
- No IAM users were listed.
- Twelve IAM roles were observed.
- One role, `AccountFullAccessRole`, had the `AdministratorAccess` policy attached.
- The role's trust relationship was restricted to the AWS service principal `account-access.amazonaws.com`.

The administrative policy represents elevated privileges, but the review did not establish that the role was improperly accessible.

### 4. CloudTrail Event Investigation
Reviewed AWS CloudTrail Event history in `us-east-2`.

Identified management events including:
- `CreateBucket`
- `PutBucketEncryption`

Examined the `PutBucketEncryption` event and confirmed that it was recorded as a write operation with no error code displayed.

CloudTrail Event history provided visibility into management activity. S3 object-level data-event logging was not verified.

## Risk Assessment

| Security Area | Observation | Assessment |
|---|---|---|
| S3 Public Access | Anonymous test request denied | Control verified for tested object |
| Data Encryption | SSE-S3 enabled | Control verified |
| IAM Privileges | Administrative permissions observed on a service-trusted role | Further review recommended |
| Audit Logging | CloudTrail management events available | Basic audit visibility verified |
| S3 Object-Level Logging | Data-event logging not verified | Potential monitoring gap |
| Threat Detection | GuardDuty not enabled during the lab | Recommended for future evaluation |

## Security Recommendations
1. Continue enforcing S3 Block Public Access unless public access is explicitly required.
2. Maintain encryption at rest for stored objects.
3. Periodically review IAM permissions and trust relationships using least-privilege principles.
4. Evaluate CloudTrail S3 data-event logging for environments requiring object-level auditing.
5. Consider GuardDuty and CloudWatch alerting for additional threat detection and monitoring, with attention to service costs.

## Conclusion
This project demonstrated practical AWS cloud security assessment techniques, including access-control verification, encryption review, IAM inspection, and CloudTrail event analysis.

The assessment confirmed several functioning security controls and identified areas for further monitoring and review. No exploitable vulnerability was demonstrated during the lab.

## Evidence
Screenshots documenting the assessment are stored in the `screenshots/` directory.

## Tools & Technologies
Amazon Web Services (AWS), Amazon S3, AWS IAM, AWS CloudTrail, Cloud Security Assessment, Risk Assessment, and Access Control Testing.
