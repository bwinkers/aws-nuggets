# Create a Security OU

## Get the Root OU id

```bash
aws organizations list-roots
```

output:

```bash
{
    "Roots": [
        {
            "Id": "r-aul3",
            "Arn": "arn:aws:organizations::xxxxxxxxxxxx:root/o-8mudmvsna8/r-abcd",
            "Name": "Root",
            "PolicyTypes": [
                {
                    "Type": "AISERVICES_OPT_OUT_POLICY",
                    "Status": "ENABLED"
                },
                {
                    "Type": "BACKUP_POLICY",
                    "Status": "ENABLED"
                },
                {
                    "Type": "TAG_POLICY",
                    "Status": "ENABLED"
                },
                {
                    "Type": "SERVICE_CONTROL_POLICY",
                    "Status": "ENABLED"
                }
            ]
        }
    ]
}
```

```bash
export PARENTID=r-abcd
aws organizations create-organizational-unit --parent-id PARENTID --name Security
```

