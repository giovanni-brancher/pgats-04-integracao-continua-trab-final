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
- Gera um relatório de testes no formato XML (JUnit)
- Armazena o relatório como **artifact** no GitHub Actions

---

## Conceitos utilizados

- **Integração Contínua (CI):** prática de integrar e validar código automaticamente a cada alteração, reduzindo riscos e acelerando o feedback.
- **GitHub Actions:** plataforma de automação nativa do GitHub, baseada em workflows declarativos em YAML.
- **Workflows e Jobs:** um workflow contém um ou mais jobs que são executados em runners (máquinas virtuais fornecidas pelo GitHub).
- **Triggers (gatilhos):** eventos que disparam a execução do workflow (`push`, `workflow_dispatch`, `schedule`).
- **Artifacts:** arquivos gerados durante a execução da pipeline e armazenados para consulta posterior (ex.: relatório de testes).
- **Testes automatizados:** validação do comportamento do código de forma automatizada, parte fundamental do processo de CI.

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
package.json
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