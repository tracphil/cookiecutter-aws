# {{ cookiecutter.region }}-vpc-{{ cookiecutter.account | lower }}-{{ cookiecutter.vpc }}

```shell script
cd /Volumes/samsung/work/occs-aws/CloudFormation/Infrastructure/Networking
```

## Create NAT Gateway and Bamboo EIP's

```shell script
aws cloudformation create-stack --template-body file://eip-allocation-retain.yml --cli-input-json file://param-files/{{ cookiecutter.region }}-vpc-{{ cookiecutter.account | lower }}-{{ cookiecutter.vpc }}/vpc-{{ cookiecutter.account | lower }}-{{ cookiecutter.vpc }}-eip-ngw.json --tags file://../common-tags-infrastructure.json

aws cloudformation create-stack --template-body file://eip-allocation-retain.yml --cli-input-json file://param-files/{{ cookiecutter.region }}-vpc-{{ cookiecutter.account | lower }}-{{ cookiecutter.vpc }}/vpc-{{ cookiecutter.account | lower }}-{{ cookiecutter.vpc }}-eip-bamboo.json --tags file://../common-tags-infrastructure.json
```

## Create the VPC

```shell script
aws cloudformation create-stack --template-body file://generic-vpc.yaml --cli-input-json file://param-files/{{ cookiecutter.region }}-vpc-{{ cookiecutter.account | lower }}-{{ cookiecutter.vpc }}/vpc-{{ cookiecutter.account | lower }}-{{ cookiecutter.vpc }}.json --tags file://../common-tags-infrastructure.json
```

## Create Private Subnets for Bamboo and Lambdas

```shell script
aws cloudformation create-stack --template-body file://generic-SubnetsRouting.yaml --cli-input-json file://param-files/{{ cookiecutter.region }}-vpc-{{ cookiecutter.account | lower }}-{{ cookiecutter.vpc }}/vpc-{{ cookiecutter.account | lower }}-{{ cookiecutter.vpc }}-subnets-routing.json --tags file://../common-tags-infrastructure.json
```

## Create Private Application Subnets

```shell script
aws cloudformation create-stack --template-body file://generic-SubnetsRouting-Apps.yaml --cli-input-json file://param-files/{{ cookiecutter.region }}-vpc-{{ cookiecutter.account | lower }}-{{ cookiecutter.vpc }}/vpc-{{ cookiecutter.account | lower }}-{{ cookiecutter.vpc }}-subnets-{{ cookiecutter.pAppName | lower }}.json --tags file://../common-tags-infrastructure.json
```
