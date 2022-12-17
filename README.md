# Lab IaC (Infrastructure as Code) com Terraform, Ansibe e AwS

Esse projeto é um Lab de IaC (Infrastructure as Code) com as tecnologia Terraform, Ansibe, AWS e Linux ubuntu.

O objetivo do Lab é gerenciar e controlar a sua infraestrutura, seja ambiente de desenvolvimento ou em ambiente de produção, através de código de forma prática, objetiva e muito mais simples com as ferramentas Terraform, Ansible e AWS.

Informativo
* [Terraform]: é uma ferramenta de software de infraestrutura como configuração de código aberto criada pela HashiCorp.
* [Ansible]: é um conjunto de ferramentas de software que permite infraestrutura como código. É de código aberto e o pacote inclui provisionamento de software, gerenciamento de configuração e funcionalidade de implantação de aplicativos.
* Windows Subsystem for Linux (WSL): Instalar o WSL no Windows 10, permiti uma instancia do Linux rodando no Windows, acessando os arquivos e facilitando a vida de desenvolvedores e administradores de sistemas.


# Preparando o ambiente

* Script ambiente-terraform.sh - Preparação ambiente Terraform - Ansible - Linux Ubutun
  ```sh
    #!/bin/bash
    #Ambiente para o IaC - Infrastructure as code

    #Instalando Terraform
    sudo apt update
    echo "Intalando Terraform"
    curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
    sudo apt-add-repository "deb [arch=$(dpkg --print-architecture)] https://apt.releases.hashicorp.com $(lsb_release -cs) main"

    #Instalando Python
    sudo apt install python3

    #Instalando Ansible no Linux - Ubutun
    sudo apt install software-properties-common
    sudo add-apt-repository --yes --update ppa:ansible/ansible
    sudo apt-get install ansible
    echo "Fim instalações ambiente IaC com Terraforme, Python e Ansible!"
  ```


* Script aws-cli.sh - Preparação ambinte AWS CLI - Linux Ubutun

  ```sh
    #!/bin/bash

    #Instalação depencias do AWS. glibc, groff e less
    echo "Iniciando instalação AWS CLI e suas dependencias...."
    sudo apt install glibc-source -y
    sudo apt install groff -y
    sudo apt install less -y

    #Baixar o instalador do AWS CLI. Como é um zip, é necessário instalar o zip no linux
    sudo apt install zip -y
    
    #Instalação AWS CLI
    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
    unzip -u awscliv2.zip
    sudo ./aws/install
    echo "Fim instalação AWS CLI!"
  ```


* Depois de instalar o AWS CLI, é necessário configurar as chaves de acesso.  

  Caso não tenha a chave de acesso da AWS, entre no link [security_credentials], vá em “criar chave de acesso” na aba “credenciais do AWS IAM”.

  Execute o comando para configurar a chave de acesso no AWS CLI local
  ```sh
    aws configure
  ```
  
  
# Inicializando o Terraform

* Entrar na home do usuário e fazer o clone do projeto
  ```sh
    $ cd ~
    $ git clone https://github.com/romarioviana/iac-terraform-aws.git
  ```
* Entrar no diretório iac-terraform-aws do projeto baixado.
   ```sh
     $ cd iac-terraform-aws
  ```

* Observer que tem os seguintes arquivos <b>main.tf</b> (arquivo com as configurações do Terraform)

Podemos iniciar o Terraform com o comando abaixo, ele vai baixar algumas configurações, alguns plug-ins para podermos utilizar o nosso provedor.
```sh
  $ terraform init
```
Obs.: Só é necessário executar esse comando se alterarmos algo no bloco terraform {} do arquivo <b>main.tf</b>


O próximo comando é para vermos o que vai acontecer quando realmente executarmos. Ele vai executar esse planejamento e exibir no os passos no terminal.
```sh
  terraform plan
```

Agora o próximo comando irá executar e aplicar o plano com as configuraçõe. O terraform irá criar a instância na AWS. Ele vai nos trazer a mesma tela do que vai acontecer.
```sh
  terraform apply
```
  

<!-- MARKDOWN LINKS & IMAGES -->
[security_credentials]: https://console.aws.amazon.com/iam/home?#/security_credentials
[Terraform]: https://developer.hashicorp.com/terraform
[Ansible]: https://www.ansible.com/
