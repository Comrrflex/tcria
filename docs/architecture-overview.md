# TCRIA — evolução prática para SaaS no Azure

## O que falta para virar SaaS

Hoje o repositório se comporta mais como um produto técnico / engine governado. Para virar SaaS de verdade, ainda faltam estas camadas:

- aplicação web online estável;
- banco persistente;
- login e gestão de usuários;
- armazenamento de arquivos;
- histórico de execuções/auditorias;
- planos/cobrança;
- observabilidade e segurança;
- deploy reprodutível.

## Arquitetura recomendada no Azure

### Fase 1 — colocar no ar rápido

Usar a stack mínima para operação real com baixo custo de complexidade:

- **Azure App Service** para hospedar a API FastAPI;
- **GitHub Actions** para deploy automático;
- **Azure Database for PostgreSQL Flexible Server** para persistência;
- **Azure Storage (Blob)** para PDFs e artefatos;
- **Application Insights** para logs, métricas e rastreabilidade operacional.

A Microsoft mantém um tutorial específico de **FastAPI + PostgreSQL no App Service**, que encaixa bem com a estrutura atual do TCRIA.

### Fase 2 — virar SaaS real

Adicionar gradualmente as capacidades de produto:

- autenticação de usuários;
- multi-tenant (cada cliente separado);
- painel com histórico de casos;
- fila para processamentos longos;
- billing;
- ambientes separados de staging e produção.

## Minha recomendação prática

Sequência sugerida para execução:

1. Subir a API no App Service.
2. Conectar PostgreSQL.
3. Guardar uploads e relatórios no Blob Storage.
4. Configurar deploy via GitHub Actions.
5. Expor uma UI simples para upload + histórico.
6. Só depois adicionar cobrança e multiempresa.

Esse caminho tende a ser mais rápido e mais barato do que iniciar já com microserviços.

- **App Service**: melhor escolha para colocar app Python online rapidamente.
- **Azure Container Apps**: passa a fazer mais sentido quando houver necessidade de containers customizados, workers separados, jobs e escalabilidade mais avançada.

## Referências oficiais (Microsoft)

- FastAPI + PostgreSQL no Azure App Service:
  https://learn.microsoft.com/en-us/azure/app-service/tutorial-python-postgresql-app-fastapi
- Python no Azure App Service (quickstart):
  https://learn.microsoft.com/en-us/azure/app-service/quickstart-python
- Deploy no App Service com GitHub Actions (Python):
  https://learn.microsoft.com/en-us/azure/developer/python/python-web-app-github-actions-app-service
- Application Insights (visão geral):
  https://learn.microsoft.com/en-us/azure/azure-monitor/app/app-insights-overview
