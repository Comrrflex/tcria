# TCRIA — caminho direto de produto técnico para SaaS

Hoje o TCRIA parece mais um **produto técnico / pipeline governado** do que um SaaS pronto.

Para virar SaaS, a evolução precisa acrescentar explicitamente a camada de serviço:

- hospedagem web contínua;
- banco persistente;
- autenticação de usuários;
- cobrança/plano;
- armazenamento de arquivos;
- observabilidade;
- deploy previsível.

## Arquitetura recomendada agora: A + B

A melhor decisão neste estágio não é “ou isto ou aquilo”.
É **A + B**:

### A) Colocar a API no Azure agora (time-to-online)

Objetivo: colocar a aplicação Python/FastAPI online rápido, com risco controlado.

- Hospedar a API em **Azure App Service**.
- Configurar deploy contínuo com **GitHub Actions**.
- Publicar uma primeira operação online para validação real de uso.

### B) Evoluir em seguida para SaaS de verdade

Objetivo: transformar a base técnica em plataforma de serviço recorrente.

Próximas capacidades:

1. banco e modelo de dados de produto (execuções, usuários, tenants);
2. login e gestão de identidade;
3. billing/plano e limites por conta;
4. armazenamento durável de arquivos e artefatos;
5. observabilidade de produção (logs, métricas, alertas);
6. pipeline de deploy previsível com ambientes e rollback.

## O caminho mais direto

1. **Fase imediata:** App Service para FastAPI + GitHub Actions.
2. **Fase seguinte:** completar a camada SaaS (banco, login, billing e painel).

Esse caminho reduz o tempo para ficar online sem travar a evolução para um SaaS completo.

## Referências oficiais (Microsoft)

- Quickstart para deploy de app Python (Django/Flask/FastAPI) no App Service:
  https://learn.microsoft.com/en-us/azure/app-service/quickstart-python
- Tutorial FastAPI + PostgreSQL no Azure App Service:
  https://learn.microsoft.com/en-us/azure/app-service/tutorial-python-postgresql-app-fastapi
- Deploy de app Python no App Service com GitHub Actions:
  https://learn.microsoft.com/en-us/azure/developer/python/python-web-app-github-actions-app-service
