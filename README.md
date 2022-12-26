# Lab de IaC (Infrastructure as Code) com Terraform, Ansibe e AwS

Nesse Lab de **Infraestrutura como código**, iremos replicar ambientes e entender como automatizar a instalação de uma máquina, instalando as dependências necessárias através de ferramentas de provisionamento. E para isso iremos utiliza as tecnologias / ferramentas Terraform, Ansible e AWS CLI, EC2 - AWS e Linux Ubuntu.

O objetivo é criar uma instância de uma máquina no EC2 da AWS com o sistema operacional Ubuntu, configurar as chaves de segurança da EC2 para permitir o acesso a instância no EC2 via SSH, acessar a instância via SSH, montar um servidor Python2 e suas dependências (Virtualenv, Django, Django rest) em um ambiente virtualizado, configura o hosts do Django para permitir o acesso de qualquer IP e por fim, acessar o acessar a página de boas vindas do DJango na internet.

O que faremos: 
* Instalação e configuração das ferramentas Terraform, Ansible e AWS CLI;
* Criação dos arquivos necessários para o Terroform;
* Criação dos arquivos necessários do Ansible;
* Criar infraestrutura na EC2 da AWS, utilizado o Terraform para criar a instância do servidor (SO ubuntu) na EC2 - AWS;
* Configura o servidor para ser acessado via SSH.
* Executar comandos dentro das máquinas durante a sua criação;
* Fazer o provisionamento com o Ansible, instalando dependências e bibliotecas, modificando arquivos e executando comandos;
* Assim, teremos o ambiente preparado e configurado através de código de forma prática, objetiva e simpla. Com gerenciamento dos pacotes e com as aplicações necessárias para o um time de desenvolvimento começar o seu trabalho que será o de desenvolver uma aplicação em ```DJango```. 


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
    echo "Intalando Terraform"
    curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
    sudo apt-add-repository "deb [arch=$(dpkg --print-architecture)] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
    sudo apt update
    sudo apt-get install terraform

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

  Caso não tenha a chave de acesso da AWS, entre no link [Security credentials EC2 - AWS], vá em “criar chave de acesso” na aba “credenciais do AWS IAM”.

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
  
  
# Acesse a WiKi para ver como fazer esse ```Lab de IaC (Infrastructure as Code)```

Na [Wiki Projeto] tem toda a documentação, onde é explicamos com detalhes todos os passos do ```Lab de IaC (Infrastructure as Code) com Terraform, Ansibe e AwS```.


# Contribuindo
As contribuições são o que torna a comunidade de código aberto um lugar incrível para aprender, inspirar e criar. Quaisquer contribuições que você fizer são muito apreciadas.

Se você tiver uma sugestão para melhorar isso, bifurque o repositório e crie uma pull request.

1. Fork o Projeto
2. Crie o seu Branch Feature (git checkout -b feature/amazing-feature)
3. Commit sua alterações (git commit -m 'Add some amazing-feature')
4. Push para o Branch (git push origin feature/amazing-feature)
5. Abra um Pull Request


---

Referências:
* [Wiki Projeto]
* [Documentação Terraform]
* [Documentação Terraform para AWS]
* [Documentação Terraform criando infrastrutura AWS]
* [AWS Account]
* [AWS CLI]
* [Configurando credenciais para o AWS CLI]
* [Security credentials EC2 - AWS]
* [Terraform]
* [Ansible]
* [How Ansible Works ]
* [Ansible Exercises ]
* [Instalar o Ansible]
* [Instalar o Python ]


:rocket::rocket::rocket:


<!-- MARKDOWN LINKS & IMAGES -->
[Wiki Projeto]: ../../wiki
[Documentação Terraform]: http://terraform.io/
[Documentação Terraform para AWS]: https://developer.hashicorp.com/terraform/tutorials/aws-get-started
[Documentação Terraform criando infrastrutura AWS]: https://developer.hashicorp.com/terraform/tutorials/aws-get-started/aws-build
[Security credentials EC2 - AWS]: https://console.aws.amazon.com/iam/home?#/security_credentials
[Terraform]: https://developer.hashicorp.com/terraform
[Ansible]: https://www.ansible.com/
[Configurando credenciais para o AWS CLI]: https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html
[AWS Account]: https://aws.amazon.com/free
[AWS CLI]: https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html
[Instalar o Ansible]: https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html#installing-ansible-on-ubuntu
[Instalar o Python ]: https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#control-node-requirements
[How Ansible Works ]: https://www.ansible.com/overview/how-ansible-works
[Ansible Exercises ]: https://github.com/ansible/workshops/tree/devel/exercises/

