# Hackathon - SOAT1 - Grupo 13 </h1>

![GitHub](https://img.shields.io/github/license/dropbox/dropbox-sdk-java)

# Resumo do projeto
Este projeto foi desenvolvido em C# com .NET 6, seguindo os princípios da arquitetura hexagonal. É um trabalho que está sendo realizado durante nossa pós-graduação com intuito de conclusão do curso, com o objetivo de aplicar as melhores práticas de arquitetura de software.

O principal objetivo deste projeto é desenvolver uma API REST para atender as demandas de uma grande corporação que visa migrar seu sistema de registro de ponto para a nuvem. Na primeira versão do produto (MVP 1), focamos em funcionalidades essenciais que permitem aos colaboradores registrar pontos, visualizar registros diários e solicitar espelhos de ponto. Além dos requisitos funcionais, damos grande ênfase aos aspectos não funcionais, como escalabilidade, segurança e alta disponibilidade, adotando tecnologias e práticas atuais do mercado para assegurar uma solução confiável e eficiente.

Sinta-se à vontade para entrar em contato conosco se tiver alguma dúvida ou sugestão. Agradecemos pelo interesse em nosso projeto!

> :construction: Projeto em construção :construction:

License: [MIT](License.txt)

# Vídeo

No vídeo abaixo, explicamos com mais detalhes o projeto:

TODO -> Link do vídeo
![Video_explicativo](<http://>)

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
As chamadas que requerem autenticação são detalhadas na documentação. Para obter um token Bearer, você pode através do seguinte projeto: [https://github.com/SOAT1-GRP13/Hackathon-Auth](https://github.com/SOAT1-GRP13/Hackathon-Auth).

**Postman**

Você pode baixar nossa Collection nos arquivos presentes na pasta Documentos/Postman

# 📒 Documentação da API

Nos projetos foi instalado o REDOC e pode ser acessado através do caminho http://localhost:[PORTA]/api-docs/index.html

# Fluxogramas

**Desenho da solução MVP**

Abaixo um breve detalhamento de cada microserviço

- **Auth-service**: Microserviço de controle de acesso dos colaboradores. No token será armazenado o id do colaborador e seu email.
- **Ponto-service**: Microserviço de controle de batidas de ponto do período em aberto. Podendo ser escalado/replicado de acordo com a carga de acesso em determinados horários.
Sua comunicação do o Relatorio-service será feito através de mensageria.
- **Relatorio-service**: Microserviço de geração de relatórios. Nele irá conter os dados dos perídos fechados, não impactando a performace das batidas do período aberto.

![fluxo_bater_ponto](</Documentos/Imagens/MVP1/fluxo_bater_ponto.png>)

![fluxo_visualizar_batidas](</Documentos/Imagens/MVP1/fluxo_visualizar_batidas.png>)

![fluxo_solicitar_espelho](</Documentos/Imagens/MVP1/fluxo_solicitar_espelho.png>)

**Desenho da solução evolutiva (fase 2)**

Abaixo um breve detalhamento de cada microserviço

- **Auth-service**: Microserviço de controle de acesso dos colaboradores. No token será armazenado o id do colaborador, seu email e role de acesso, se é apenas colaborador ou supervisor.
- **Ponto-service**: Microserviço de controle de batidas de ponto do período em aberto. Podendo ser escalado/replicado de acordo com a carga de acesso em determinados horários. Nessa etapa ele irá receber a funcionalidade de permitir o colaborar alterar uma batida. Será implementado uma tela administrativa para o supervisor poder aprovar ou reprovar as solicitações de alteração de batida e gerar relatórios.
Sua comunicação do o Relatorio-service e Notificacao-service será feito através de mensageria.
- **Relatorio-service**: Microserviço de geração de relatórios. Nele irá conter os dados dos perídos fechados, não impactando a performace das batidas do período aberto.
- **Notificacao-service**: Microserviço responsável por notificar os usuários sobre batidas de ponto pendentes, solicitação de aprovação de alteração de batidas de ponto e confirmação se a solicitação de alteração de batidade de ponto foi aprovada ou não.

![fluxo_editar_ponto](</Documentos/Imagens/MVP2/fluxo_editar_ponto.png>)

![fluxo_aprovar_edicao_ponto](</Documentos/Imagens/MVP2/fluxo_aprovar_edicao_ponto.png>)

![fluxo_notificar_usuario](</Documentos/Imagens/MVP2/fluxo_notificar_usuario.png>)

![fluxo_gerar_relatorio](</Documentos/Imagens/MVP2/fluxo_gerar_relatorio.png>)

![fluxo_inserir_usuario](</Documentos/Imagens/MVP2/fluxo_inserir_usuario.png>)

# Clean Architecture

Nesse projeto decidimos utilizar a arquitetura Clean Architecture e devido à natureza específica do framework .Net, adotamos uma nomeclatura diferente para nossa estrutura que segue os princípios da Clean Architecture (Arquitetura Limpa).

Na nossa arquitetura, a camada de Controller corresponde à Camada de API da Clean Architecture. Esta camada é responsável por lidar com as requisições externas e coordenar o fluxo de dados.

A camada de queries foi concebida como a camada de Gateways na Clean Architecture. Aqui, centralizamos a lógica relacionada à recuperação de dados, permitindo uma separação clara entre a fonte de dados e a lógica de negócios.

Para a implementação das operações de comando, optamos por utilizar a camada de command handlers, que equivale à camada de controller na Clean Architecture. Nesta camada, tratamos as ações e comandos vindos da camada de API, garantindo a execução das operações necessárias.

O projeto de Domain abriga as nossas entidades de negócio e objetos de valor (Value Objects). Esta camada é o coração do nosso sistema, encapsulando as regras de negócio essenciais.

No contexto da persistência de dados, a camada de Infraestrutura (Infra) foi designada como a camada de DB (Banco de Dados) na Clean Architecture. Aqui, lidamos com aspectos de armazenamento e recuperação de dados, mantendo a separação entre as preocupações de banco de dados e as regras de negócio.

Esta arquitetura foi adotada para promover a manutenibilidade, escalabilidade e testabilidade do nosso projeto, permitindo uma clara separação de responsabilidades em cada camada. Estamos comprometidos em seguir os princípios da Clean Architecture para alcançar um sistema robusto e bem estruturado.

# Microserviços

Adotamos a arquitetura de microserviços devido à sua capacidade de oferecer escalabilidade e alta disponibilidade, fundamentais para o sucesso do nosso sistema de ponto eletrônico em nuvem. Principais benefícios incluem:

- **Escalabilidade**: Permite ajustar recursos por serviço conforme necessário, otimizando a eficiência durante picos de demanda.
- **Resiliência**: Isola falhas, garantindo que um problema em um serviço não comprometa todo o sistema.
- **Desenvolvimento Ágil**: Facilita atualizações e a adição de novas funcionalidades, com equipes trabalhando de forma independente em serviços distintos.
- **Tecnologia Diversificada**: Cada serviço pode utilizar a stack tecnológica mais adequada, promovendo inovação.
  
Esta estrutura nos prepara para atender às necessidades atuais e futuras, mantendo o sistema robusto e adaptável.

**Repositório de nossos Microserviços**

- **Auth**: https://github.com/SOAT1-GRP13/Hackathon-Auth
- **Ponto**: https://github.com/SOAT1-GRP13/Hackathon-Ponto
- **Relatório**: https://github.com/SOAT1-GRP13/Hackathon-Relatorio

**Fluxo de comunicação entre os microserviços**

![fluxo_microservicos](</Documentos/Imagens/fluxo_microservicos-Hackathon.png>)

# Sonar
Para assegurar um bom padrão de qualidade do código e manter a integridade de nossos microserviços, optamos por integrar o SonarQube em nosso processo de desenvolvimento. O SonarQube é uma plataforma de inspeção contínua da qualidade do código, que nos permite monitorar e melhorar a qualidade do código ao longo do tempo, identificando:
- **Bugs**: O SonarQube ajuda a detectar e corrigir bugs no código antes que eles cheguem à produção, reduzindo potencialmente o tempo de inatividade e melhorando a experiência do usuário.
- **Vulnerabilidades de Segurança**: Ao analisar o código em busca de vulnerabilidades conhecidas, o SonarQube nos permite fortalecer a segurança de nossos microserviços, protegendo dados sensíveis e sistemas contra ataques.
- **Code Smells**: A identificação de problemas de design no código, nos ajuda a manter o código limpo e mais fácil de manter, facilitando a integração de novas funcionalidades.

**Integração com CI/CD**

A integração do SonarQube com nossas pipelines de CI/CD (Integração Contínua e Entrega Contínua/Deploy Contínuo) automatiza a análise de código em cada push ou pull request na main, garantindo que apenas o código que atende aos nossos padrões de qualidade seja promovido para os ambientes subsequentes. Essa integração nos permite:

**Feedback Instantâneo**: Desenvolvedores recebem feedback imediato sobre a qualidade do código, permitindo correções rápidas e iterativas.
**Visibilidade da Qualidade do Código**: Dashboards e relatórios gerados pelo SonarQube oferecem uma visão clara da saúde do código e das áreas que necessitam de atenção, promovendo uma cultura de qualidade entre a equipe.

**Link dos nossos microserviços no Sonar**

- **Auth**: https://sonarcloud.io/summary/overall?id=SOAT1-GRP13_Hackathon-Auth
- **Ponto**: https://sonarcloud.io/summary/overall?id=SOAT1-GRP13_Hackathon-Ponto
- **Relatório**: https://sonarcloud.io/summary/overall?id=SOAT1-GRP13_Hackathon-Relatorio

# Esteira de publicação (CI/CD)

Nossos projetos adotam o GitHub Actions para automatizar a esteira de CI/CD, dividida em duas etapas principais, garantindo uma entrega contínua e eficiente:

**1. Criação e Armazenamento de Imagens Docker**
- **Criação de Imagem**: Utilizamos o Dockerfile na raiz de cada projeto para construir imagens Docker, encapsulando o microserviço.
- **Armazenamento**: As imagens são automaticamente enviadas para o Docker Hub, proporcionando uma gestão centralizada e facilitando o acesso e a distribuição.

**2. Publicação na AWS**
- **Deploy**: Na sequência, o GitHub Actions é configurado para implantar a imagem Docker mais recente na nossa infraestrutura AWS, utilizando serviços como ECS (Elastic Container Service) ou EKS (Elastic Kubernetes Service), dependendo da necessidade do projeto.
- **Automação**: Todo o processo é automatizado, desde a integração do código até o deploy, assegurando que as novas versões sejam lançadas rapidamente e com estabilidade.

Esta estratégia de CI/CD nos permite manter um ritmo constante de inovação e melhorias, reduzindo significativamente o tempo de colocação no mercado de novas funcionalidades e correções.

**Link das imagens dos nossos microserviços no DockerHub**

- **Auth**: https://hub.docker.com/repository/docker/christiandmelo/hackathon-soat1-grp13-auth/general
- **Ponto**: https://hub.docker.com/repository/docker/christiandmelo/hackathon-soat1-grp13-ponto/general
- **Relatório**: https://hub.docker.com/repository/docker/christiandmelo/hackathon-soat1-grp13-relatorio/general

# Comunicação Assíncrona com RabbitMQ

A escolha do RabbitMQ como nosso broker de mensagens para a comunicação assíncrona entre os microserviços foi motivada por sua robustez, flexibilidade e ampla adoção no mercado. Como uma solução open source, o RabbitMQ oferece:

- **Confiabilidade**: Garante a entrega de mensagens mesmo em caso de falhas de rede ou serviços, através de funcionalidades como confirmações de mensagens e filas duráveis.
- **Escalabilidade**: Facilmente escalável, suporta o crescimento da carga de trabalho sem comprometer o desempenho.
- **Compatibilidade**: Sua ampla adoção no mercado assegura uma vasta gama de bibliotecas e integrações, facilitando a implementação em diversos ambientes de desenvolvimento.

Utilizando o RabbitMQ, promovemos um menor acoplamento entre os serviços, aumentando a resiliência e a eficiência do sistema como um todo.

# Gestão da Infraestrutura na AWS com Terraform

A escolha do Terraform para gerir nossa infraestrutura na AWS reflete nosso compromisso com práticas modernas de desenvolvimento e operações. O Terraform, sendo uma ferramenta de infraestrutura como código (IaC) open-source, nos permite:

- **Automatizar a Criação**: Automatizamos a criação, modificação e remoção de recursos na AWS, reduzindo o potencial para erros humanos e aumentando a eficiência.
- **Gerenciar como Código**: Mantemos a configuração da nossa infraestrutura versionada e documentada, facilitando as revisões e alterações.
- **Implantar com Confiança**: Utilizamos os planos de execução do Terraform para revisar as alterações antes de aplicá-las, garantindo que apenas as mudanças desejadas sejam feitas.
- **Adaptabilidade**: O Terraform nos permite gerenciar uma ampla variedade de recursos na AWS, proporcionando a flexibilidade para adaptar e escalar nossa infraestrutura conforme as necessidades do projeto evoluem.

Através do Terraform, asseguramos uma abordagem consistente e reproduzível para a gestão da infraestrutura, essencial para suportar a operação contínua e o crescimento do nosso sistema de ponto eletrônico em nuvem.

**Desenho da nossa infraestrutura na AWS**

TODO -> Colocar o desenho da nossa infraestrutura
![infra_AWS](</Documentos/Imagens//.png>)

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
