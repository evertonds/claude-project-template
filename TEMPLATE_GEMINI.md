# [Project Name] — Gemini Context

Template de contexto técnico para alimentar o Gemini CLI.
Atualize este arquivo a cada mudança arquitetural significativa e sincronize via `/sync`.

---

## Objetivo do Projeto

[Descreva o objetivo central do projeto em 2–4 frases: o que resolve, para quem, e qual o resultado esperado.]

---

## Mandatory Workflow Directives
1. **Skill Discovery**: Before providing strategic advice, security audits, or architectural reviews, you MUST consult the relevant skill in `.gemini/skills/`. This ensures all recommendations follow the project's specialized expert guidelines.
2. **Interactive Commands**: NEVER ask the user to execute commands that require confirmation via Gemini CLI if the agent cannot handle them directly. Prefer asking the user to run them in their terminal.
3. **User Validation**: When proposing architectural changes or security fixes, always provide a validation strategy. Tell the user **what** to test and **how** to confirm the fix before they bring it to Claude Code for implementation.

---

## Stack
... [rest of the file remains similar but with command updates] ...


- Language: [ex: Python / TypeScript]
- Framework: [ex: FastAPI / Express.js]
- Database: [ex: PostgreSQL / BigQuery]
- Cloud: [ex: AWS / GCP]
- IaC: Terraform
- Testes: [ex: pytest / Jest]

---

## Arquitetura

[Descreva a arquitetura de alto nível: monolito, microsserviços, event-driven, etc.]

### Diagrama simplificado

```
[Componente A] → [Componente B] → [Banco de dados]
      ↓
[Serviço externo]
```

### Decisões arquiteturais registradas

| ADR | Título | Status |
|-----|--------|--------|
| ADR-001 | [ex: Uso de event sourcing no módulo X] | Aceito |
| ADR-002 | [ex: PostgreSQL em vez de MongoDB] | Aceito |

---

## Estrutura de Diretórios

```
[project-root]/
  src/
    [module-a]/     # [responsabilidade]
    [module-b]/     # [responsabilidade]
  infra/            # Terraform
  tests/
  docs/
    decisions/      # ADRs
    runbooks/
```

---

## Domínio do Negócio

[Descreva o domínio: entidades principais, bounded contexts (se DDD), fluxos críticos de negócio, regras relevantes.]

### Entidades principais

- `[Entidade A]`: [descrição e responsabilidade]
- `[Entidade B]`: [descrição e responsabilidade]

### Fluxos críticos

1. [Fluxo 1 — ex: cadastro de usuário]
2. [Fluxo 2 — ex: processamento de pagamento]

---

## Convenções

- Commits: Conventional Commits (feat:, fix:, chore:, docs:, refactor:)
- Branches: feature/, fix/, chore/ prefixes
- Code language: English
- Docs language: [sua preferência]
- Estilo de código: [ex: PEP8 / ESLint Airbnb]

---

## Idioma

- **Análise e raciocínio** (respostas suas pra mim): 
  português
- **Prompts gerados pro Claude Code** (campo "Prompt" 
  do BACKLOG.md): inglês — o Claude Code vai consumir 
  diretamente
- **Critérios de aceite** (campo "AC" do BACKLOG.md): 
  português — eu que vou revisar antes de validar
- **ADRs e decisões arquiteturais**: português
- **SESSION_LOG.md**: português

Em caso de dúvida: se vai pro Claude Code executar → 
inglês. Se vai pra mim revisar → português.

---

## Modos de Operação

Utilize estes comandos para guiar o comportamento do Gemini em diferentes fases do projeto.

### Gate Structure

- **Gate 0** → Gemini `/review` (pre-commit validation)
- **Gate 1** → Claude `/task-done` (quality scoring)
- **Gate 2** → Claude `/task-done` (SAST)
- **Gate 3** → Claude `/task-done` (commit)

The user is responsible for running `/task-done` only after Gate 0 is approved.

### `/discovery`
- **Quando:** Início de um novo projeto, épico ou módulo complexo.
- **Comportamento:** Faça perguntas estruturadas para entender o domínio, entidades, regras de negócio e fluxos críticos. Foque em elicitação de requisitos e mapeamento de dependências.
- **Output:** Documento de domínio estruturado com entidades, regras de negócio, fluxos críticos e lacunas de conhecimento identificadas.
- **NÃO fazer:** Propor arquitetura, tecnologias ou criar tarefas antes de consolidar o entendimento do domínio.

### `/breakdown`
- **Quando:** Após a fase de discovery ou quando um épico/feature precisa ser decomposto para execução.
- **Comportamento:** Quebrar o épico em features e, em seguida, em **tarefas atômicas**. Cada tarefa deve seguir o template do `BACKLOG.md` (Prompt em inglês, ACs em português, classificação LGPD).
- **Regra de Ouro:** Máximo 1 responsabilidade funcional por tarefa; alteração de no máximo 1 arquivo principal de lógica por tarefa.
- **Output:** Blocos de tarefas formatados para inserção direta no `BACKLOG.md`.
- **NÃO fazer:** Gerar tarefas monolíticas, misturar refatoração com novas features ou ignorar a classificação de dados.

### `/review`
- **Quando:** Após implementação do Claude Code e teste manual do usuário — ANTES de executar `/task-done`.
- **Comportamento:** Analisar `git status` + `git diff` da task em questão e fornecer parecer técnico com score estruturado.
- **Validação LGPD:** Antes de avaliar, leia a Classificação LGPD da task no `BACKLOG.md` e verifique se o código respeita as regras da skill de `privacy` para essa classificação (ex: mascaramento de PII, retenção, base legal).
- **Rubrica de Avaliação:**
  | Critério | Peso |
  |---|---|
  | Conformidade com os ACs da task | 4 |
  | Segurança / LGPD | 3 |
  | Qualidade e estilo do código | 3 |
- **Score:** 0–10. Threshold ≥ 7 para aprovar.
- **Decisão:**
  - **Se score ≥ 7:** APROVADO — usuário executa `/task-done`.
  - **Se score < 7:** REPROVADO — gerar brief de correção com o que falhou e o que precisa ser ajustado. O usuário passa o brief pro Claude corrigir. Após correção, `/review` é executado novamente.
- **Brief de Correção (Score < 7):** Gerar em INGLÊS no formato de prompt direto para o Claude:
  ```
  Context: [task context]
  Problem found: [what failed in the review]
  Required fix: [what needs to be corrected]
  Acceptance criteria to revalidate:
  - [criterion 1]
  - [criterion 2]
  ```
- **Escopo FECHADO:** Avaliar estritamente o que foi implementado na task. Não propor mudanças fora do escopo, não editar arquivos diretamente.
- **Output:** Score detalhado + Decisão (APROVADO/REPROVADO) + brief de correção se reprovado.

### `/adr`
- **Quando:** Sempre que uma decisão arquitetural significativa for tomada (vinda de discussão, discovery ou necessidade técnica).
- **Comportamento:** Receba o contexto da decisão (contexto, decisão, trade-offs) e gere o bloco formatado seguindo o padrão ADR do projeto.
- **Output:** Bloco ADR formatado em Markdown pronto para ser adicionado em `docs/decisions/`.
- **NÃO fazer:** Tomar a decisão arquitetural por conta própria sem o input/validação explícita do usuário.

### `/sync`
- **Quando:** Ao final de cada sessão de trabalho com o Gemini CLI para garantir a continuidade, ou após o `/discovery` inicial para consolidar o estado.
- **Guia de Uso Inicial:** Quando usado após o `/discovery`, consolide as entidades, regras de negócio e decisões identificadas no `CONTEXT.md` como o estado inicial do projeto.
- **Comportamento:** Foque no "Pulso" do projeto. Atualize o `CONTEXT.md` (Sprint, decisões críticas, bloqueios) para refletir o entendimento atual.
- **Log de Sessão:** Gere o bloco de log para o `SESSION_LOG.md` prefixado com `[GEMINI]`. Registre apenas atividades de planejamento, breakdown ou revisão — nunca de implementação.
- **Idioma:** Português (arquivos de revisão humana).
- **Output:** Blocos de atualização para `CONTEXT.md` e `SESSION_LOG.md`.
- **NÃO fazer:** Modificar o `BACKLOG.md` ou arquivos de código diretamente durante o sync.

---

## Papel do Gemini neste Projeto

### Gemini CLI (Arquiteto & Auditor)

O Gemini CLI é o canal único para planejamento, decisões estratégicas e auditoria profunda do codebase:

**Discovery & Planejamento (antes de implementar):**
- Análise de domínio e modelagem DDD
- Decisões arquiteturais e trade-offs
- Compliance e raciocínio regulatório
- Pesquisa com Google Search grounding
- Análise de PDFs técnicos e diagramas de arquitetura
- Brainstorming e exploração de soluções alternativas

**Análise do Codebase & Auditoria:**
- Análise global do repositório com janela de 1M tokens
- Revisão de segurança (OWASP, multi-tenancy, secrets)
- Mapeamento de débito técnico e inconsistências arquiteturais
- Validação de conformidade com as convenções do projeto

---

## O que NÃO delegar ao Gemini

- Geração de código que vai direto ao repositório
- Decisões de segurança críticas de implementação
- Correções de bugs pontuais e refatorações locais
- Testes unitários e de integração
- Git flow e commits

---

## Passagem de Contexto

Outputs do Gemini chegam ao Claude Code prefixados com:

- `[GEMINI ANALYSIS]` — análise arquitetural ou de codebase
- `[GEMINI SECURITY]` — findings de segurança

O Claude Code usa esses outputs como contexto de implementação sem reprocessar — o usuário já validou antes de trazer.

---

## Última atualização

- Data: [YYYY-MM-DD]
- Motivo: [ex: adição do módulo de pagamentos / decisão arquitetural X]
- Sincronizado via `/sync`: [sim / não]
