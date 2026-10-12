TF_Log : details output of transaction based on third party api.
terraform import vs terraform taints or -replace="aws_instance.test" 
- taints delete & recreate the entire resource & update the state file
- import maps the infra with the resource block & update the state file
Terraform Secrets vs hardcoding.
- Mapping from secrets value from secret manager.
- mark sensitive as true.
- use random_passord to generate a token.
Count vs for each :
- count will be index only on interger.
- but for each can be support string & fomation as well for resource indexing.
drift detection:
- 
