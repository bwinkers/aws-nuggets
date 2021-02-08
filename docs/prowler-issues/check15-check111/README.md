# Secure IAM password policies

```bash
 1.5  [check15] Ensure IAM password policy requires at least one uppercase letter (Scored)   
       FAIL! Password Policy missing upper-case requirement 

 1.6  [check16] Ensure IAM password policy require at least one lowercase letter (Scored)   
       FAIL! Password Policy missing lower-case requirement 

 1.7  [check17] Ensure IAM password policy require at least one symbol (Scored)   
       FAIL! Password Policy missing symbol requirement 

 1.8  [check18] Ensure IAM password policy require at least one number (Scored)   
       FAIL! Password Policy missing number requirement 

 1.9  [check19] Ensure IAM password policy requires minimum length of 14 or greater (Scored)   
       FAIL! Password Policy missing or weak length requirement 

 1.10  [check110] Ensure IAM password policy prevents password reuse: 24 or greater (Scored)   
       FAIL! Password Policy missing reuse requirement 

 1.11  [check111] Ensure IAM password policy expires passwords within 90 days or less (Scored)   
       FAIL! Password expiration is not set 
```

Run this:

```bash
aws --profile admin-email \
iam update-account-password-policy \
--minimum-password-length 14 \
--require-symbols \
--require-numbers \
--require-uppercase-characters \
--require-lowercase-characters \
--allow-users-to-change-password  \
--max-password-age 90 \
--password-reuse-prevention 24 \
--hard-expiry 
```
