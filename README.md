# 🔐 AWS Security Monitoring & Compliance Lab

## Overview
Implementation of comprehensive security monitoring using AWS native services for audit, compliance, and threat detection.

## 🎯 Objectives
- Monitor AWS resources and user activities in real-time
- Set up automated alerts for suspicious activities
- Create audit trails for compliance requirements
- Analyze logs for security insights

## 🏗️ Architecture
![Security Monitoring Architecture](images/security-monitoring-arch.png)

## 🔧 Technologies & Services
- **Amazon CloudWatch** (Metrics, Alarms, Dashboards)
- **AWS CloudTrail** (API activity logging)
- **Amazon Athena** (Log querying and analysis)
- **AWS IAM** (User activity tracking)
- **Amazon S3** (Log storage with encryption)
- **Amazon SNS** (Alert notifications)

## 📁 Repository Structure

## 🚀 Implementation

### 1. CloudWatch Monitoring Setup
- Created custom metrics for security events
- Configured alarms for:
  - Unauthorized API calls
  - Root account usage
  - Security group changes
  - IAM policy modifications
- Built CloudWatch dashboard for security overview

### 2. CloudTrail Configuration
- Enabled multi-region CloudTrail logging
- Configured log file validation (integrity checking)
- Set up S3 bucket with encryption for log storage
- Created Athena tables for SQL querying of CloudTrail logs

### 3. Alerting & Response
- Configured SNS topics for security alerts
- Implemented Lambda functions for automated response
- Created runbooks for common security incidents

## 🔐 Security Monitoring Rules Implemented
| Rule | Service | Purpose |
|------|---------|---------|
| Root Account Usage | CloudTrail | Alert on root account activity |
| IAM Policy Changes | CloudTrail | Track permission modifications |
| Security Group Changes | CloudTrail | Monitor network access changes |
| Failed Logins | CloudTrail | Detect brute force attempts |
| Unusual API Activity | CloudWatch | Anomaly detection |

## 📊 Sample Athena Queries for Security Analysis
```sql
-- Find all failed console logins
SELECT eventTime, userIdentity.arn, errorMessage
FROM cloudtrail_logs
WHERE eventName = 'ConsoleLogin'
AND errorMessage IS NOT NULL;

-- Detect IAM policy changes
SELECT eventTime, userIdentity.arn, eventName, requestParameters
FROM cloudtrail_logs
WHERE eventName LIKE '%Policy%'
OR eventName LIKE '%Role%';
