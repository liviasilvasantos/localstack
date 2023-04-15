# Estudos de localstack

Material de apoio: https://thomsdacosta.medium.com/localstack-ambiente-local-para-testar-a-sua-aplica%C3%A7%C3%A3o-aws-4bc255e3ab56

## Profile

Se nenhum profile for informado, será criado um profile default.
Caso crie um profile, será necessário sempre informar ele nos comandos com --profile <nome>.

Os profiles podem ser verificados em: <home>/.aws/config.

Também é possível utilizar o pacote awslocal, que utilizará host, porta e profiles padrões.

## Criar configuração - profile default  

> aws configure  
    AWS Access Key ID [None]: fakeAccessKeyId
    AWS Secret Access Key [None]: fakeSecretAccessKey
    Default region name [None]: sa-east-1
    Default output format [None]: json

## Criar configuração - profile coruja  

> aws configure --profile coruja

## Criar secret no secret manager  

> aws --endpoint http://localhost:4566 secretsmanager \
    create-secret --name databasePassword \
    --description "Segredo para efetuar um teste com LocalStack" \
    --secret-string "db123" \
    --region sa-east-1

## Listar identity do profile  

> aws --endpoint http://localhost:4566 sts get-caller-identity  

## Criar bucket S3  

> aws --endpoint http://localhost:4566 s3 mb s3://coruja  
    make_bucket: coruja

## Adicionar arquivo ao bucket S3  

> aws --endpoint http://localhost:4566 s3 cp coruja.txt s3://coruja   
    upload: ./coruja.txt to s3://coruja/coruja.txt

## Listar arquivos do bucket S3  

> aws --endpoint http://localhost:4566 s3 ls s3://coruja  

## Download de um arquivo do bucket S3  

> aws --endpoint http://localhost:4566 s3 cp s3://coruja/coruja.txt tmp   
    download: s3://coruja/coruja.txt to tmp/coruja.txt