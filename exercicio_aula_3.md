# Exercício Aula 03 - Deployments e Releases

Neste exercício vamos criar um fluxo de deployment e release para uma aplicação web utilizando o GitHub Actions e Azure Web Apps.

## Exercício 1 - Criando o fluxo de release

- Faça o fork deste repositório para o seu usuário
- Baseado no conteúdo demonstrado durante a aula, crie um novo branch no seu repositório chamado `exercicio-aula-3`
- Crie um commit adicionando um arquivo de texto na raiz do repositório com o nome `nova_feature.txt`(o arquivo pode estar vazio)
- Adicione uma nova mensagem de commit como se fosse uma nova feature
- Edite o arquivo `README.md` e adicione uma nova mensagem de commit como se fosse uma correção de bug
- Abra um Pull Request para o branch `main` com as alterações
- Faça o merge do Pull Request
- Observe a criação de uma nova release no seu repositório

## Exercício 2 - Fazendo o deploy da nossa aplicação

### Configurando o ambiente Azure

Para este exercício vamos utilizar o Azure Web Apps para hospedar nossa aplicação web. Para isso, vamos criar um novo recurso no Azure chamado Web App. Para isso, acesse o portal do Azure e crie um novo recurso do tipo Web App. Para este exercício, vamos utilizar o plano de serviço gratuito, mas você pode utilizar o plano de serviço pago se preferir.

- **Nome do recurso**: `exercicio-ci-cd-fiap` (Criar novo)
- **Nome do App**: `exercicio-aula-3-<seu_usuario_github>`
- **Publish**: `Code`
- **Runtime Stack**: `Node 16 LTS`
- **Linux plan**: `Exercicios-FIAP` (Criar novo)
- **Pricing Tier**: `Basic B1`
- **GitHub Actions settings**: `Enable continuous deployment`
- **Conexão com o GitHub**:
  - Autorizar
  - Selecionar o seu usuário
  - Selecionar o repositório `sample-blog`
  - Branch: `main`
  - Selecione para utilizar o arquivo `main_exercicio-aula-3.yml` do repositório
- **Clique em `Review + Create` e em seguida em `Create`**
- Espere :clock1: até que o recurso seja criado
- Baixe o `Publish Profile` clicando em `Download publish profile`
- Salve seu conteúdo como um Secret no GitHub com o nome `AZURE_WEBAPP_PUBLISH_PROFILE`

### :warning: Corrigindo problemas de permissão

Se você estiver utilizando o plano de serviço gratuito, provavelmente irá receber um erro de permissão ao tentar fazer o deploy da aplicação. Para corrigir isso, vamos adicionar o usuário o seu usuário como `Owner` do resource group.
- Selecione o resource group criado
- Vá no menu `Access Control (IAM)`
- Clique em `Add`
- Em seguida em `Add role assignment`
- Selecione `Owner` no campo `Role`
- Na aba `Members`, selecione o seu usuário clicando em `Select members`
- Clique em `Review + assign`
