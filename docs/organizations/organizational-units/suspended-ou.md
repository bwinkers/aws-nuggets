# Create an OU for Supended Accounts

## Create the OU via Control Tower Console

If this is done via CLI it will not be registered in Control Tower.
Get the new OU id from the console.

## Create and attach a zero permissions SCP

### Create the DenyALL policy

```bash
aws organizations create-policy \
--content  file://deny-all-policy.json \
--description "Denies all actions. Used to secure suspended accounts" \
--name DenyALL \
--type SERVICE_CONTROL_POLICY \
--profile prod-master
```

###

Get the policy ID from the response

```bash
{
    "Policy": {
        "PolicySummary": {
            "Id": "p-12ab34cd",
```    

### Attach the DenyALL policy to the Suspended OU

```bash
aws organizations attach-policy \
--policy-id  p-12ab34cd \
--target-id ou-abcd-suspendedou \
--profile prod-master
```
