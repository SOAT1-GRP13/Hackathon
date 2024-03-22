# Hackathon - SOAT1 - Grupo 13 </h1>

![GitHub](https://img.shields.io/github/license/dropbox/dropbox-sdk-java)

# Resumo do projeto
Este projeto foi desenvolvido em C# com .NET 6, seguindo os princípios da arquitetura hexagonal. É um trabalho que está sendo realizado durante nossa pós-graduação com intuito de conclusão do curso, com o objetivo de aplicar as melhores práticas de arquitetura de software.

O propósito principal do projeto é criar uma API REST para atender as necessidades de uma .....

Sinta-se à vontade para entrar em contato conosco se tiver alguma dúvida ou sugestão. Agradecemos pelo interesse em nosso projeto!

> :construction: Projeto em construção :construction:

License: [MIT](License.txt)

# 🛠️ Abrir e rodar o projeto utilizando o docker

Para o correto funcionamento precisa do docker instalado.

Com o docker instalado, acesse a pasta raiz do projeto e execute o comando abaixo: 

```shell
docker-compose up
```

O arquivo docker-compose.yaml incluído neste projeto é projetado para automatizar o processo de construção e implantação de nossa arquitetura de microserviços. Ao executar este docker-compose, ele iniciará um conjunto de contêineres Docker, seguindo uma estrutura bem definida: um contêiner individual para cada microserviço descrito no projeto, além de contêineres dedicados para os bancos de dados associados a esses microserviços, sempre que aplicável. Isso assegura um isolamento eficaz das dependências e facilita a gestão de recursos.

Adicionalmente, o arquivo docker-compose está encarregado de instanciar um contêiner para o RabbitMQ, que atua como nosso intermediário de mensagens Este setup garante que as filas necessárias sejam criadas dinamicamente conforme os microserviços são ativados e interagem uns com os outros.

Cada microserviço, ao ser inicializado, é responsável por executar suas próprias 'migrations', criando as tabelas necessárias e inserindo registros de exemplo, estabelecendo assim o estado inicial requerido para que o sistema funcione corretamente.

# ⌨️ Testando a API

Você pode testar esta API de duas maneiras: usando o Postman ou o Swagger, que está configurado no projeto.

**Swagger**:

Para acessar o Swagger do projeto localmente, utilize o seguinte link:
- Auth - http://localhost:5270/swagger/index.html
- Ponto - http://localhost:5271/swagger/index.html
- Relatório - http://localhost:5272/swagger/index.html
  
O Swagger já contém exemplos de chamadas com dados reais.

Se estiver testando via Swagger, lembre-se de adicionar o token obtido na resposta da chamada no menu "Authorize".
Autenticação:
As chamadas que requerem autenticação são detalhadas na documentação. Para obter um token Bearer, você pode através do seguinte projeto: [https://github.com/SOAT1-GRP13/TechChallenge-SOAT1-GRP13-Auth](https://github.com/SOAT1-GRP13/Hackathon-Auth).

**Postman**

Você pode baixar nossa Collection nos arquivos presentes na pasta Documentos/Postman

# 📒 Documentação da API

Nos projetos foi instalado o REDOC e pode ser acessado através do caminho http://localhost:[PORTA]/api-docs/index.html

# Fluxogramas

**Desenho da solução MVP**

![fluxo_microservicos](</Documentos/Imagens/MVP1/fluxo_bater_ponto.png>)

![fluxo_microservicos](</Documentos/Imagens/MVP1/fluxo_visualizar_batidas.png>)

![fluxo_microservicos](</Documentos/Imagens/MVP1/fluxo_solicitar_espelho.png>)

**Desenho da solução evolutiva (fase 2)**

![fluxo_microservicos](</Documentos/Imagens/MVP2/fluxo_editar_ponto.png>)

![fluxo_microservicos](</Documentos/Imagens/MVP2/fluxo_aprovar_edicao_ponto.png>)

![fluxo_microservicos](</Documentos/Imagens/MVP2/fluxo_notificar_usuario.png>)

![fluxo_microservicos](</Documentos/Imagens/MVP2/fluxo_gerar_relatorio.png>)

![fluxo_microservicos](</Documentos/Imagens/MVP2/fluxo_inserir_usuario.png>)

# Clean Architecture

Devido à natureza específica do framework .Net, adotamos uma nomeclatura diferente para nossa estrutura que segue os princípios da Clean Architecture (Arquitetura Limpa).

Na nossa arquitetura, a camada de Controller corresponde à Camada de API da Clean Architecture. Esta camada é responsável por lidar com as requisições externas e coordenar o fluxo de dados.

A camada de queries foi concebida como a camada de Gateways na Clean Architecture. Aqui, centralizamos a lógica relacionada à recuperação de dados, permitindo uma separação clara entre a fonte de dados e a lógica de negócios.

Para a implementação das operações de comando, optamos por utilizar a camada de command handlers, que equivale à camada de controller na Clean Architecture. Nesta camada, tratamos as ações e comandos vindos da camada de API, garantindo a execução das operações necessárias.

O projeto de Domain abriga as nossas entidades de negócio e objetos de valor (Value Objects). Esta camada é o coração do nosso sistema, encapsulando as regras de negócio essenciais.

No contexto da persistência de dados, a camada de Infraestrutura (Infra) foi designada como a camada de DB (Banco de Dados) na Clean Architecture. Aqui, lidamos com aspectos de armazenamento e recuperação de dados, mantendo a separação entre as preocupações de banco de dados e as regras de negócio.

Esta arquitetura foi adotada para promover a manutenibilidade, escalabilidade e testabilidade do nosso projeto, permitindo uma clara separação de responsabilidades em cada camada. Estamos comprometidos em seguir os princípios da Clean Architecture para alcançar um sistema robusto e bem estruturado.

#Microserviço

Decidimos utilizar microserviço nesse projeto devido.........

**Fluxo de comunicação entre os microserviços**

![fluxo_microservicos](</Documentos/Imagens/fluxo_microservicos-Hackathon.png>)

# Sonar
Nossos microserviços estão sendo

# Esteira de publicação

# RabbitMQ

# TerraForm

# Relatório de Impacto à Proteção de Dados Pessoais (RIPD)

O relatório pode ser acessado através do link: 
- https://soat1-grp13.github.io/

# Relatório OWASP Zap

O relatório pode ser acessado através do link:
- https://soat1-grp13.github.io/

# ✔️ Tecnologias utilizadas

- ``.Net 6``
- ``Postgres``
- ``Docker``
- ``RabbitMQ``
- ``TerraForm``
- ``AWS``


# Autores

| [<img src="https://avatars.githubusercontent.com/u/28829303?s=400&v=4" width=115><br><sub>Christian Melo</sub>](https://github.com/christiandmelo) |  [<img src="https://avatars.githubusercontent.com/u/89987201?v=4" width=115><br><sub>Luiz Soh</sub>](https://github.com/luiz-soh) |  [<img src="https://avatars.githubusercontent.com/u/21027037?v=4" width=115><br><sub>Wagner Neves</sub>](https://github.com/nevesw) |  [<img src="https://avatars.githubusercontent.com/u/34692183?v=4" width=115><br><sub>Mateus Bernardi Marcato</sub>](https://github.com/xXMateus97Xx) |
| :---: | :---: | :---: | :---: |
