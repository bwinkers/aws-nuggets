# [check120] Ensure a support role has been created to manage incidents with AWS Support (Scored)

## Verify broken

```bash
./prowler -c check120 -p admin-email
```

Result:

```bash
1.20  [check120] Ensure a support role has been created to manage incidents with AWS Support (Scored)   
       FAIL! Support Policy not applied to any Role 
```

## Fix 

### Create a user

```bash
aws iam create-user --user-name breakglassSupportIncidentUser
```

Result:

```bash

    "User": {
        "Path": "/",
        "UserName": "breakglassSupportIncidentUser",
        "UserId": "AI*****************",
        "Arn": "arn:aws:iam::##########:user/breakglassSupportIncidentUser",
        "CreateDate": "2021-02-08T00:39:32+00:00"
    }
}
```

You will need the Arn returned for the TrustPolicy file.

```bash
arn:aws:iam::##########:user/breakglassSupportIncidentUser
```

### Create the Trust Policy file

```bash
{
    "Version": "2012-10-17",
    "Statement": [
      {
        "Effect": "Allow",
        "Principal": {
          "AWS": "arn:aws:iam::##########:user/breakglassSupportIncidentUser"
        },
        "Action": "sts:AssumeRole"
      }
    ]
  }
```

### Create the Role

```bash
aws --profile admin-email iam create-role --role-name CompanySupportIncidentRole --assume-role-policy-document file://TrustPolicy.json
```

Response:

```bash
{
    "Role": {
        "Path": "/",
        "RoleName": "CompanySupportIncidentRole",
        "RoleId": "AR****************",
        "Arn": "arn:aws:iam::##########:role/CompanySupportIncidentRole",
        "CreateDate": "2021-02-08T00:43:22+00:00",
        "AssumeRolePolicyDocument": {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Effect": "Allow",
                    "Principal": {
                        "AWS": "arn:aws:iam::##########:user/breakglassSupportIncidentUser"
                    },
                    "Action": "sts:AssumeRole"
                }
            ]
        }
    }
}
```

Attach the standard AZWS policy for support incident management.

```bash
aws --profile admin-email iam attach-role-policy --policy-arn "arn:aws:iam::aws:policy/AWSSupportAccess" --role-name CompanySupportIncidentRole
```

## Check your work

```bash
./prowler -c check120 -p admin-email
```

Result:

```bash
1.20  [check120] Ensure a support role has been created to manage incidents with AWS Support (Scored)   
       PASS! Support Policy attached to CompanySupportIncidentRole
```
