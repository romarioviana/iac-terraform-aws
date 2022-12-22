# Lab IaC (Infrastructure as Code) com Terraform, Ansibe e AwS

Esse projeto é um Lab de IaC (Infrastructure as Code) com as tecnologia Terraform, Ansibe, AWS e Linux ubuntu.

Objetivo é criar infraestrutura na EC2 da AWS, utilizado o Terraform para criar a instância do servidor (SO ubuntu) na EC2. E para provisionar o servidor foi utilizado o Ansible na criação de um servidor Python3 com todas as sua dependências (Virtualenv, Django, Django rest) e na configuração do hosts do Python para permite o acesso de qualquer IP. 
Assim, teremos o ambiente preparado e configurado através de código de forma prática, objetiva e simpla, para que o desenvolver possa subir a sua Python.


Informativo:
* [Terraform]: é uma ferramenta de software de infraestrutura como configuração de código aberto criada pela HashiCorp.
* [Ansible]: é um conjunto de ferramentas de software que permite infraestrutura como código. É de código aberto e o pacote inclui provisionamento de software, gerenciamento de configuração e funcionalidade de implantação de aplicativos.
* Windows Subsystem for Linux (WSL): Instalar o WSL no Windows 10, permiti uma instancia do Linux rodando no Windows, acessando os arquivos e facilitando a vida de desenvolvedores e administradores de sistemas.
* Não esquecer de remover as instâncias na ECE da AWS após os testes para evitar cobrança indesejadas. 



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
  
  A AWS CLI armazena as informações de credenciais especificadas com o comando ```aws configure``` em um arquivo local chamado ```credenciais```, na pasta chamada ```.aws ``` em seu diretório home. As opções de configuração menos confidenciais especificadas com o comando ```aws configure``` são armazenadas em um arquivo local chamado ```config```, também armazenado na pasta ```.aws``` em seu diretório home.

  Por exemplo, os arquivos gerados pela AWS CLI para um profile padrão configurado com ```aws configure``` são semelhantes ao seguinte no SO linux.
  ```sh
    ~/.aws/credentials
  ```
  Veja mais informações em [Configurando credenciais para o AWS CLI].
  
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



# Contribuindo
As contribuições são o que torna a comunidade de código aberto um lugar incrível para aprender, inspirar e criar. Quaisquer contribuições que você fizer são muito apreciadas.

Se você tiver uma sugestão para melhorar isso, bifurque o repositório e crie uma pull request.

1. Fork o Projeto
2. Crie o seu Branch Feature (git checkout -b feature/amazing-feature)
3. Commit sua alterações (git commit -m 'Add some amazing-feature')
4. Push para o Branch (git push origin feature/amazing-feature)
5. Abra um Pull Request


<!-- MARKDOWN LINKS & IMAGES -->
[security_credentials]: https://console.aws.amazon.com/iam/home?#/security_credentials
[Terraform]: https://developer.hashicorp.com/terraform
[Ansible]: https://www.ansible.com/
[Configurando credenciais para o AWS CLI]: https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html
