# Automação AWS usando Ansible

Projeto que utiliza o Ansible para automatizar a criação de instâncias EC2 na AWS.
## Estrutura do repositório:
```
├── LICENSE
├── README.md
├── hosts
├── main.yml                         >> Chama as tarefas
└── roles                            >> Estrutura do Ansible
    └── creating-instances
        ├── defaults
        │   └── main.yml
        ├── handlers
        │   └── main.yml
        ├── meta
        │   └── main.yml
        ├── README.md
        ├── tasks                    >> Tarefas
        │   ├── main.yml
        │   └── provisioning.ylm     >> .yml que contém as tarefas que serão executadas
        ├── tests
        │   ├── inventory
        │   └── test.yml
        └── vars
            └── main.yml             >> Arquivo de variáveis do provisioning.ylm 
```
## Requisitos

- [Ubuntu](https://ubuntu.com)
- [AWS](https://aws.amazon.com)
- [Ansible](https://www.ansible.com)

## Preparação do Ambiente

### Instalação do Ansible:

```bash
$ sudo apt-get update
$ sudo apt-get install ansible
```
### Instalação AWS CLI:

```bash
$ sudo apt-get update
$ sudo apt-get install awscli
```
### Criação de usuário na AWS no IAM
```bash
- No Console da AWS, vá para o serviço IAM (Identity and Access Management).
- Crie um novo usuário, atribua-o ao grupo "Admin" para permissões administrativas.
- Após criar o usuário, acesse suas configurações e crie uma chave de acesso Command Line Interface (CLI).
- Anote a "Access Key ID" e a "Secret Access Key" geradas para usar na etapa seguinte.
```
### Configuração AWS CLI:
```bash
$ aws configure
```
```bash
$ AWS Access Key ID [None]: (ID da Chave de Acesso da AWS)
$ AWS Secret Access Key [None]: (Chave de Acesso Secreta da AWS)
$ Default region name [us-east-1]: (Nome da região padrão)
$ Default output format [None]: (Formato de saída padrão)
```
As informações inseridas serão salvas no arquivo de configuração da AWS (~/.aws/config e ~/.aws/credentials). Esses arquivos contêm as configurações essenciais para interações futuras com os serviços AWS.

## Como utilizar?
1- Clone o repositório.
```bash
$ git clone https://github.com/rocoxta/ansible-aws.git
```
2- Edite as variáveis no arquivo main.yml da pasta vars de acordo com sua necessidade:
```bash
security_group_name: Nome do Security Group a ser criado.
profile: Perfil AWS configurado no seu arquivo de credenciais.
region: Região da AWS onde os recursos serão provisionados.
instance_type: Tipo de instância EC2.
image: AMI (Amazon Machine Image) a ser usada para a instância EC2.
keypair: Nome da chave SSH configurada na AWS.
count: Número de instâncias EC2 a serem criadas.
```
Execute o playbook Ansible:
```bash
$ ansible-playbook main.yml
```
## O playbook "provisioning.yml" realizará as seguintes tarefas:

- Criação de um Security Group na AWS permitindo tráfego SSH.
- Criação de instância EC2 associada ao Security Group.
- Adição da instância ao inventário temporário.
- Atualização do arquivo de hosts com o IP público e privado da instância.
- Aguardo até que a instância esteja disponível via SSH.
- Adição de uma tag na instância.

## Referências
- [Ansible Galaxy](https://docs.ansible.com/ansible/latest/galaxy/dev_guide.html)
- [Amazon Web Services Guide](https://docs.ansible.com/ansible/latest/collections/amazon/aws/docsite/guide_aws.html#ansible-collections-amazon-aws-docsite-aws-intro)
- [EC2 Group: Maintain an ec2 VPC security group](https://docs.ansible.com/ansible/2.9/modules/ec2_group_module.html)
- [EC2: Create, terminate, start or stop an instance in ec2](https://docs.ansible.com/ansible/2.9/modules/ec2_group_module.html)
## Autor
👤 **Rodrigo Costa**


