# Exercício Aula 03 - Deployments e Releases

Neste exercício vamos criar um fluxo de deployment e release para uma aplicação web utilizando o GitHub Actions e Azure Web Apps.

## Configurando o ambiente Azure

Para este exercício vamos utilizar o Azure Web Apps para hospedar nossa aplicação web. Para isso, vamos criar um novo recurso no Azure chamado Web App. Para isso, acesse o portal do Azure e crie um novo recurso do tipo Web App. Para este exercício, vamos utilizar o plano de serviço gratuito, mas você pode utilizar o plano de serviço pago se preferir.

- **Nome do recurso**: `exercicio-ci-cd-fiap` (Criar novo)
- **Nome do App**: `exercicio-aula-3`
- **Publish**: `Code`
- **Runtime Stack**: `Node 18 LTS`
- **Linux plan**: `Exercicios-FIAP` (Criar novo)
- **Pricing Tier**: `Basic B1`
- **GitHub Actions settings**: `Enable continuous deployment`
- **Conexão com o GitHub**:
  - Autorizar
  - Selecionar o seu usuário
  - Selecionar o repositório `octodex-feed-app`
  - Branch: `main`
- **Clique em `Review + Create` e em seguida em `Create`**
- Espere :clock1: até que o recurso seja criado
- Na aba `Configuraton`, clique em `General Settings` e depois em cole os seguintes comandos no campo `Startup Command`:
  - `npm install`
  - `npm run build`
  - `npm run start`
- A aplicação irá reiniciar, aguarde e depois clique para ver o app criado

### Corrigindo problemas de permissão

Se você estiver utilizando o plano de serviço gratuito, provavelmente irá receber um erro de permissão ao tentar fazer o deploy da aplicação. Para corrigir isso, vamos adicionar o usuário o seu usuário como `Owner` do resource group.
- Selecione o resource group criado
- Vá no menu `Access Control (IAM)`
- Clique em `Add`
- Em seguida em `Add role assignment`
- Selecione `Owner` no campo `Role`
- Na aba `Members`, selecione o seu usuário clicando em `Select members`
- Clique em `Review + assign`

## Criando o fluxo de release