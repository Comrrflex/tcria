# TCRIA arquitetura de evolução para SaaS

## Diagnóstico atual

Hoje o TCRIA está mais próximo de um **produto técnico/governado** do que de um SaaS completo:

- pipeline orientado a processamento e governança;
- execução por CLI/API;
- geração de artefatos auditáveis;
- pouca camada de serviço contínuo para usuários finais.

## Camadas que faltam para SaaS real

Para operar como SaaS de forma consistente, a plataforma precisa incorporar explicitamente:

- hospedagem web contínua;
- banco persistente;
- autenticação de usuários;
- cobrança/planos;
- armazenamento de arquivos;
- observabilidade;
- deploy previsível.

## Arquitetura recomendada: A + B (não "ou")

### Fase A — colocar online rápido no Azure

Objetivo: publicar a API atual com baixo atrito e ganhar operação real em produção.

- Hospedar a aplicação Python/FastAPI no **Azure App Service**.
- Configurar deploy contínuo por **GitHub Actions**.
- Expor endpoints para uso interno/early adopters.

Resultado esperado: sistema online rapidamente, com operação controlada e ciclos curtos de validação.

### Fase B — evoluir para SaaS completo

Objetivo: transformar o produto técnico em serviço multiusuário comercializável.

Evoluções recomendadas:

1. **Dados e persistência**
   - banco relacional gerenciado (ex.: Azure Database for PostgreSQL);
   - versionamento e retenção de metadados de execução.

2. **Identidade e segurança**
   - login de usuários (OIDC / Microsoft Entra ID B2C ou equivalente);
   - separação por organização/tenant;
   - RBAC para operações sensíveis.

3. **Arquivos e artefatos**
   - armazenamento em objeto (ex.: Azure Blob Storage);
   - trilha de custódia e políticas de retenção.

4. **Billing e planos**
   - controle de consumo por tenant;
   - integração de cobrança e limites por plano.

5. **Observabilidade e confiabilidade**
   - logs estruturados, métricas e traces;
   - SLO/SLI, alertas e runbooks.

6. **Entrega previsível**
   - ambientes separados (dev/staging/prod);
   - migrações de banco automatizadas;
   - estratégia de rollback.

## Caminho mais direto

A sequência mais pragmática agora é:

1. **A (agora):** publicar a API no Azure App Service para ter presença online imediata.
2. **B (em seguida):** adicionar as capacidades de SaaS (banco, login, billing, painel e operação contínua).

Essa abordagem reduz time-to-production sem bloquear a construção do modelo SaaS definitivo.
