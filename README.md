# Trabalho Final — Integração Contínua para Automação de Testes

[![CI](https://github.com/giovanni-brancher/pgats-04-integracao-continua-trab-final/actions/workflows/ci.yml/badge.svg)](https://github.com/giovanni-brancher/pgats-04-integracao-continua-trab-final/actions/workflows/ci.yml)

Trabalho de conclusão da disciplina de **Integração Contínua para Automação de Testes** da pós-graduação.

---

## Sobre o projeto

Implementação de uma pipeline de Integração Contínua com **GitHub Actions** aplicada a um projeto Node.js com testes automatizados. O projeto utiliza a classe `ServicoDePagamento`, desenvolvida na disciplina de Programação para Automação de Testes, como base para a execução dos testes.

---

## Solução implementada

A pipeline está definida em `.github/workflows/ci.yml` e contempla:

| Gatilho | Descrição |
|---|---|
| `push` | Executa automaticamente a cada novo commit enviado ao repositório |
| `workflow_dispatch` | Permite execução manual pela interface do GitHub Actions |
| `schedule` | Execução agendada diariamente (cron) |

A pipeline é composta por **4 jobs independentes** executados em paralelo:

| Job | Descrição |
|---|---|
| `lint` | Verifica qualidade de código com **ESLint** |
| `audit` | Detecta vulnerabilidades nas dependências com `npm audit` |
| `test` | Executa os testes em matrix **Node 18, 20 e 22**, gerando relatórios JUnit, cobertura (nyc) e HTML (mochawesome) |
| `deploy-pages` | Publica o relatório mochawesome no **GitHub Pages** (somente na branch `master`) |

O relatório HTML interativo está disponível em: https://giovanni-brancher.github.io/pgats-04-integracao-continua-trab-final/

---

## Conceitos utilizados

- **Integração Contínua (CI):** prática de integrar e validar código automaticamente a cada alteração, reduzindo riscos e acelerando o feedback.
- **GitHub Actions:** plataforma de automação nativa do GitHub, baseada em workflows declarativos em YAML.
- **Workflows e Jobs:** um workflow contém um ou mais jobs que são executados em runners (máquinas virtuais fornecidas pelo GitHub).
- **Triggers (gatilhos):** eventos que disparam a execução do workflow (`push`, `workflow_dispatch`, `schedule`).
- **Artifacts:** arquivos gerados durante a execução da pipeline e armazenados para consulta posterior (ex.: relatório de testes).
- **Testes automatizados:** validação do comportamento do código de forma automatizada, parte fundamental do processo de CI.
- **mochawesome:** reporter para Mocha que gera relatórios HTML interativos e visuais, úteis para análise local dos resultados dos testes.
- **nyc (Istanbul):** ferramenta de cobertura de código para JavaScript; mede quais linhas, funções e branches foram exercitadas pelos testes.
- **ESLint:** ferramenta de análise estática que identifica padrões problemáticos e impõe convenções de código.
- **Matrix strategy:** estratégia do GitHub Actions que executa o mesmo job em múltiplas versões de ambiente (ex.: Node 18, 20, 22) em paralelo.
- **GitHub Pages:** serviço de hospedagem estática do GitHub, usado para publicar o relatório HTML dos testes automaticamente.

---

## Estrutura do projeto

```
.github/
  workflows/
    ci.yml                      # Definição da pipeline de CI (4 jobs)
src/
  ServicoDePagamento.js         # Classe principal
test/
  ServicoDePagamento.test.js    # Testes unitários (Mocha)
mochawesome-report/             # Relatório HTML gerado localmente (ignorado pelo git)
test-results/                   # Relatório XML gerado no CI (ignorado pelo git)
coverage/                       # Relatório de cobertura gerado localmente (ignorado pelo git)
package.json
.mocharc.json                   # Configuração do Mocha
eslint.config.mjs               # Configuração do ESLint
```

---

## Pré-requisitos

- [Node.js](https://nodejs.org/) 18 ou superior
- npm

## Instalação

```bash
npm install
```

## Executando os testes localmente

```bash
npm test
```

## Verificando qualidade de código (lint)

```bash
npm run lint
```

## Gerando relatório de cobertura de código

```bash
npm run test:coverage
```

O relatório será gerado em `coverage/index.html`. Abra o arquivo no navegador para visualizar a cobertura por arquivo, linha e função.

## Gerando relatório HTML local (mochawesome)

```bash
npm run test:report
```

O relatório será gerado em `mochawesome-report/mochawesome.html`. Abra o arquivo no navegador para visualizar os resultados de forma interativa.

## Gerando relatório XML (formato CI)

```bash
npm run test:ci
```

Gera `test-results/results.xml` no formato JUnit, compatível com pipelines de CI.