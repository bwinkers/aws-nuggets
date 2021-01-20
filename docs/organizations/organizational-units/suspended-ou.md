# Create an OU for Supended Accounts

```bash
aws organizations create-organizational-unit --parent-id $PARENTID --name Suspended --profile prod-master
```

Output:

```bash
{
    "OrganizationalUnit": {
        "Id": "ou-abcd-nestedou",
        "Arn": "arn:aws:organizations::908804739064:ou/o-8mudmvsna8/ou-abcd-nestedou",
        "Name": "Suspended"
    }
}
```

## Create and attach a zero permissions SCP

### Create the DenyALL policy

```bash
  aws organizations create-policy
--content  file://deny-all-policy.json
--description "Denies all actions. Used to secure suspended accounts"
--name DenyALL
--type SERVICE_CONTROL_POLICY
```
