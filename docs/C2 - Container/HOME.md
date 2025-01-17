# C2 - Container

No segundo nível podemos verificar de forma mais detalhada como é interligada a arquitetura do Horusec e seus componentes, como também as tecnologias que fazem parte desse ecossistema.

O Horusec foi construindo utilizando usando as seguintes abordagens:
- A **Horusec-CLI** é um compilador que executa localmente na maquina do usuário seja atrávez de uma maquina de desenvolvimento ou uma esteira CI/CD em busca de vulnerabilidades. E seus containers são:
  - **Horusec-CLI:** interface de linha de comando que realiza orquestração de ferramentas de análise estática de código.
- O **Horusec-VsCode** é uma extensão da ferramenta visual studio code que utiliza a Horusec-CLI para análisar projetos em busca de vulnerabilidades. E seus containers são:
  - **Horusec-VsCode** é responsável por iniciar o horusec-cli em imagem docker e trazer o resultado da análise para dentro do Ambiente de Desenvolvimento Integrado (IDE) em um formato amigável a fim de garantir que o desenvolvedor faça suas devidas modificações.
- O **Horusec-Platform** é uma plataforma web construida em micro-serviços para visualização e gestão das vulnerabilidades. E seus containers são:
  - **API** Responsável por salvar as análises realizada via Horusec-CLI no banco de dados principal e publicar para os serviços analytic e webhook via message broker.
  - **Analytic** Responsável por receber as análises realizadas via message broker e salvar no banco de dados analytic para visualização no dasboard do container Horusec-Manager.
  - **Auth** Responsável por gerenciar sessão e acessos a plataforma web através do container Horusec-Manager.
  - **Core** Responsável por gerenciamento de repositórios, workspaces e tokens da plataforma web através do container Horusec-Manager.
  - **Manager** Responsável por disponibilizar a página estática para integração com os containers do Horusec-Platform.
  - **Messages** Responsável por diparos de emails em determida ações do usuário da plataforma web através do container Horusec-Manager.
  - **Vulnerability** Responsável por realizar a gestão das vulnerabilidades criadas pelo container Horusec-API.
  - **Webhook** Responsável por disparo de análises para serviços de terceiros via HTTP na plataforma web através do container Horusec-Manager.
- O **Horusec-Operator** é uma aplicação usando a base de kubernetes operator para agilizar e garantir que os serviços sejam entregues nos formatos desejados. E seus containers são:
  - **Horusec-Operator** é responsável por realizar a integração com o kubernetes, onde após instalado sua CRD no cluster ele pode identificar que o usuário pediu modificações e aplicar no cluster de acordo com as configurações enviadas pelo usuário.


![diagram](c2.svg)