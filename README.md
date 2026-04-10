# claude-project-template

Template base de configuração para projetos usando **Claude Code**. Inclui skills de boas práticas de engenharia e comandos prontos para uso em qualquer projeto de software, com foco em segurança multi-tenant e conformidade LGPD.

---

## Estrutura

```
.claude/
  skills/       # Conhecimento especializado (Architecture, Security, Privacy, etc.)
  commands/     # Atalhos de fluxo (/session-start, /task-done, /sync)
  settings.json # Hooks e permissões do Claude Code
.gemini/
  skills/       # Skills para o Gemini CLI (Auditoria, Pesquisa, Arquitetura)
CLAUDE.md       # Contexto do projeto para o Claude (Stack, Setup, Convenções)
GEMINI.md       # Contexto técnico para o Gemini CLI (janela de 1M tokens)
CONTEXT.md      # Estado vivo do projeto (Sprint, objetivos, bloqueios)
BACKLOG.md      # Lista de tarefas atômicas com critérios de aceite (DoR/DoD)
SESSION_LOG.md  # Registro histórico das sessões de trabalho
```

---

## Como usar este template (Guia de Instanciação)

Siga este checklist ao iniciar um novo projeto baseado neste template:

### 1. Setup de Arquivos
- [ ] Criar repositório do projeto.
- [ ] Copiar diretórios `.claude/` e `.gemini/` para a raiz.
- [ ] Copiar `TEMPLATE_CLAUDE.md` renomeando para `CLAUDE.md`.
- [ ] Criar `GEMINI.md` a partir do template correspondente.
- [ ] Criar `CONTEXT.md`, `BACKLOG.md` e `SESSION_LOG.md` a partir dos seus respectivos `.template`.

### 2. Configuração do Projeto (`CLAUDE.md`)
- [ ] Definir a **Stack** (Linguagem, Framework, DB, Cloud).
- [ ] Listar os **Comandos** reais de dev, test, build e lint.
- [ ] Configurar **Security Tool**: Escolher e testar a ferramenta SAST (ex: `njsscan`, `bandit`, `npm audit`).
- [ ] Preencher **Security Setup**: Configurar `MULTI_TENANT`, `AUTH_METHOD`, etc.
- [ ] Preencher **Privacy Setup**: Definir `LEGAL_BASIS`, `RETENTION` e campos `PII_FIELDS`.

### 3. Alinhamento Inicial
- [ ] Rodar o comando `/session-start` pela primeira vez.
- [ ] Cadastrar a primeira **Tarefa Atômica** no `BACKLOG.md`.
- [ ] Verificar se o `.gitignore` protege segredos (como `.env`).

---

## Skills

Skills são instruções especializadas que o Claude carrega dinamicamente. Algumas são ativadas **automaticamente** quando o contexto é relevante — outras você pode invocar diretamente digitando `/nome-da-skill` no Claude Code.

---

### 🏗️ `architecture`
**Quando usar:** Antes de começar qualquer feature nova, ao propor um novo módulo, ou ao avaliar trade-offs de design.

**O que faz:** Guia decisões estruturais antes de codar. Inclui princípios de arquitetura, checklist pré-implementação e formato padrão para ADRs (Architecture Decision Records).

**Como chamar:** `/architecture`

---

### 💻 `development`
**Quando usar:** Durante o desenvolvimento do dia a dia — ao escrever funções, refatorar código, revisar nomenclatura.

**O que faz:** Define convenções de código, estrutura de funções, padrões de nomenclatura, tratamento de erros e checklist antes de submeter código.

**Como chamar:** `/development`

---

### 🔒 `security`
**Quando usar:** Em toda e qualquer feature — segurança é transversal. Especialmente em fluxos multi-tenant, autenticação, endpoints de API e manipulação de segredos.

**O que faz:** Cobre secrets, isolamento de dados por tenant (B2B), autenticação, autorização, validação de inputs e OWASP Top 10.

**Como chamar:** `/security`

---

### 🔐 `privacy`
**Quando usar:** Sempre que a tarefa tocar em dados de usuários, registros pessoais, coleta, armazenamento ou exclusão de dados.

**O que faz:** Aplica princípios de *privacy-by-design* e conformidade LGPD. Inclui classificação de dados (`PERSONAL`, `SENSITIVE`), regras de retenção e minimização.

**Como chamar:** `/privacy`

---

### 🧪 `qa`
**Quando usar:** Ao escrever testes, revisar cobertura, validar uma feature antes do merge.

**O que faz:** Define a pirâmide de testes, padrões de qualidade, cobertura por tipo de código, testes de contrato de API e checklist pré-merge.

**Como chamar:** `/qa`

---

### 🗄️ `data`
**Quando usar:** Ao modelar schemas, escrever migrations, otimizar queries, construir pipelines de dados ou lidar com dados sensíveis.

**O que faz:** Padrões de modelagem, regras para migrations, boas práticas de queries, pipelines idempotentes e tratamento de PII.

**Como chamar:** `/data`

---

### ☁️ `cloud`
**Quando usar:** Ao provisionar recursos, desenhar infraestrutura, revisar políticas IAM ou trabalhar com qualquer serviço cloud. **Toda infraestrutura deve usar Terraform.**

**O que faz:** Padrões universais de IaC com Terraform, tagging obrigatório, IAM, secrets management e observabilidade.

**Como chamar:** `/cloud`

---

### 🔁 `devops`
**Quando usar:** Ao desenhar pipelines de CI/CD, configurar ambientes, planejar deploys ou trabalhar com Terraform em automação.

**O que faz:** Estratégia de ambientes, estrutura de pipelines CI/CD, gestão de secrets em pipelines e estratégia de rollback.

**Como chamar:** `/devops`

---

### 📋 `product`
**Quando usar:** Ao definir requisitos, escrever critérios de aceite, revisar escopo ou fechar uma feature.

**O que faz:** Checklist pré-implementação, formato de critérios de aceite (Given/When/Then), controle de escopo e definição de pronto (DoD).

**Como chamar:** `/product`

---

### 📝 `documentation`
**Quando usar:** Ao escrever READMEs, ADRs, runbooks, docstrings ou changelogs.

**O que faz:** Define documentos obrigatórios, estrutura de README, padrões de documentação de código e uso de diagramas.

**Como chamar:** `/documentation`

---

### 🔗 `integrations`
**Quando usar:** Ao integrar com APIs externas, implementar OAuth, tratar webhooks ou desenhar lógica de retry/fallback.

**O que faz:** Padrões de autenticação, resiliência (retry, timeout, circuit breaker), idempotência e tratamento de webhooks.

**Como chamar:** `/integrations`

---

### 🤖 `gemini`
**Quando usar:** Ao tomar decisões arquiteturais, modelar domínio, realizar análise de segurança ampla ou análise global do codebase via Gemini CLI.

**O que faz:** Define o fluxo de trabalho com o Gemini CLI (Auditor/Arquiteto). Estabelece gatilhos de sincronização (/sync) e análise profunda.

**Como chamar:** `/gemini`

---

### 🔍 `code-review`
**Quando usar:** Antes de abrir qualquer PR. Invoque para uma revisão sistemática cobrindo todas as dimensões de qualidade.

**O que faz:** Checklist completo: segurança, correção lógica, qualidade de código, testes, dados, infra e documentação.

**Como chamar:** `/code-review`

---

### 💰 `finops`
**Quando usar:** Ao provisionar recursos cloud, revisar mudanças de infraestrutura ou avaliar impacto de custos.

**O que faz:** Estimativa de custo, alertas de budget, controles de custo cloud e boas práticas de Terraform para custo.

**Como chamar:** `/finops`

---

## Commands

Commands são fluxos de trabalho manuais que automatizam processos específicos do ciclo de vida do projeto.

---

### 🏁 `/session-start`
**Quando usar:** No início de cada sessão de trabalho.

**O que faz:** Carrega o estado atual do projeto (`CONTEXT.md`), o histórico da última sessão (`SESSION_LOG.md`) e identifica a próxima tarefa pronta no `BACKLOG.md`.

```
/session-start
```

---

### ✅ `/task-done`
**Quando usar:** Ao finalizar uma tarefa para rodar os gates de qualidade e realizar o commit.

**O que faz:** Executa auto-avaliação (scoring), roda o ADR check, o SAST (ferramenta de segurança), gera mensagem de commit (Conventional Commits), exibe o diff e atualiza os logs de sessão e backlog.

```
/task-done TASK-XXX
```

---

### 🔄 `/sync`
**Quando usar:** Após decisões arquiteturais significativas, novos ADRs ou mudanças no stack para atualizar o contexto do projeto.

**O que faz:** Atualiza o `CONTEXT.md` com o estado atual (sprint, decisões, bloqueios) e realiza o append no `SESSION_LOG.md`.

```
/sync
```

---

### ✨ `/new-feature`
**Quando usar:** No início de qualquer feature nova, antes de codar.

**O que faz:** Guia o planejamento inicial — clareza de escopo, arquivos afetados, identificação de skills e criação de branch.

```
/new-feature
```

---

### ✅ `/pre-commit`
**Quando usar:** Antes de qualquer commit ou abertura de PR.

**O que faz:** Checklist rápido de qualidade pré-commit — lint, testes, typecheck e auditoria básica.

```
/pre-commit
```

---

### 🚀 `/deploy-checklist`
**Quando usar:** Antes de qualquer deploy em staging ou produção.

**O que faz:** Verificação completa pré-deploy — testes, infra, migrations, observabilidade e plano de rollback.

```
/deploy-checklist
```

---

### 🐛 `/debug`
**Quando usar:** Ao investigar bugs ou incidentes.

**O que faz:** Fluxo estruturado de debugging — reprodução, coleta de evidências, hipótese e isolamento da causa raiz.

```
/debug
```

---

### 👀 `/review`
**Quando usar:** Antes de abrir um PR.

**O que faz:** Executa a skill de code-review contra o diff atual ou arquivo especificado, gerando um checklist de bloqueadores.

```
/review
```

---

### 🔭 `/gemini-analyze` & 🔐 `/gemini-security`
**Quando usar:** Para análise global do repositório ou revisão profunda de segurança via Gemini CLI (janela de 1M tokens).

**O que faz:** Invocam o Gemini CLI para mapear débito técnico, inconsistências arquiteturais ou vulnerabilidades OWASP complexas.

```
/gemini-analyze
/gemini-security
```

---

## Customizando para seu projeto

Ao usar este template, preencha o `CLAUDE.md` com os detalhes específicos do seu projeto (Stack, Commands reais, Conventions e Known Errors). As skills e commands de fluxo fornecidos são agnósticos e projetados para funcionar em qualquer stack moderna.

---

## Referências

- [Claude Code Docs](https://code.claude.com/docs)
- [Gemini CLI Documentation](https://github.com/google/gemini-cli)
- [LGPD - Lei Geral de Proteção de Dados](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm)
