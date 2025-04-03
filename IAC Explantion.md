if I wanna create a Terraform or an IAC, I would start with modules, making sure that every resources I need is under a folder structure in the modules. Then I will link them up the enivironment, by referencing it in the environments(prod, staging and dev) as seen below. the variables(strings and numbers needed for it to work) will be inserted in the .tfvars

terraform/
├── modules/
│   ├── ec2/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── network_interface/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
|   ├── security_groups/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   └── vpc/
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
└── environments/
    ├── dev/
    │   ├── main.tf
    │   ├── variables.tf
    │   └── outputs.tf
    │   └── dev.tfvars
    ├── staging/
    │   ├── main.tf
    │   ├── variables.tf
    │   └── outputs.tf
    │   └── staging.tfvars
    └── prod/
        ├── main.tf
        ├── variables.tf
        └── outputs.tf
        └── prod.tfvars



cd into the directory of the environment, create a "<name>.tfvars" file and type this command

```shell
terraform init
terraform plan -var-file="dev.tfvars" -lock=
terraform apply -var-file="staging.tfvars" -lock=false
```
or
```shell
terraform init
terraform plan -var-file="staging.tfvars" -lock=false
terraform apply -var-file="staging.tfvars" -lock=false

```
or 
```shell
terraform init
terraform plan -var-file="prod.tfvars" -lock=false
terraform apply -var-file="staging.tfvars" -lock=false
```


to destroy

```shell
terraform destory
```
