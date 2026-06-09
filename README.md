# Trabalho Final — Integração Contínua para Automação de Testes

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

Além dos gatilhos, a pipeline:
- Executa os testes automatizados com **Mocha**
- Gera um relatório de testes no formato XML (JUnit) via `mocha-junit-reporter`
- Armazena o relatório como **artifact** no GitHub Actions

Para uso local, o projeto também oferece geração de relatório HTML interativo via **mochawesome**.

---

## Conceitos utilizados

- **Integração Contínua (CI):** prática de integrar e validar código automaticamente a cada alteração, reduzindo riscos e acelerando o feedback.
- **GitHub Actions:** plataforma de automação nativa do GitHub, baseada em workflows declarativos em YAML.
- **Workflows e Jobs:** um workflow contém um ou mais jobs que são executados em runners (máquinas virtuais fornecidas pelo GitHub).
- **Triggers (gatilhos):** eventos que disparam a execução do workflow (`push`, `workflow_dispatch`, `schedule`).
- **Artifacts:** arquivos gerados durante a execução da pipeline e armazenados para consulta posterior (ex.: relatório de testes).
- **Testes automatizados:** validação do comportamento do código de forma automatizada, parte fundamental do processo de CI.
- **mochawesome:** reporter para Mocha que gera relatórios HTML interativos e visuais, úteis para análise local dos resultados dos testes.

---

## Estrutura do projeto

```
.github/
  workflows/
    ci.yml                      # Definição da pipeline de CI
src/
  ServicoDePagamento.js         # Classe principal
test/
  ServicoDePagamento.test.js    # Testes unitários (Mocha)
mochawesome-report/             # Relatório HTML gerado localmente (ignorado pelo git)
test-results/                   # Relatório XML gerado no CI (ignorado pelo git)
package.json
.mocharc.json                   # Configuração do Mocha
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

## Gerando relatório HTML local

```bash
npm run test:report
```

O relatório será gerado em `mochawesome-report/mochawesome.html`. Abra o arquivo no navegador para visualizar os resultados de forma interativa.

## Gerando relatório XML (formato CI)

```bash
npm run test:ci
```

Gera `test-results/results.xml` no formato JUnit, compatível com pipelines de CI.