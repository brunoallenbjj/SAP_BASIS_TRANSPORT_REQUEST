# SAP Transport Request - Dicas Simples de Utilização

## 📌 O que é um Transport Request?

Um **Transport Request** nada mais é do que um conjunto de alterações ou criações de funcionalidades que são movidas de um ambiente SAP para outro, por meio de um **objeto de transporte**.

Esses objetos podem conter alterações ou criações em:

- Tabelas  
- Programas  
- Jobs  
- Processos  

---

## 📂 Tipos de Transport Request

### 🔧 Workbench Requests

- Usados para registrar **alterações em objetos do Repositório** e **Customizing** para **todos os clientes**.
- Incluem objetos como programas, classes, funções, tabelas do dicionário, etc.

### ⚙️ Customizing Requests

- Registram **configurações específicas do cliente**.
- Referem-se apenas ao cliente de origem da solicitação.
- Utilizados para alterações feitas via SPRO (Customizing).

---

## 🔁 Transações SAP Relacionadas

| Transação | Descrição |
|----------|-----------|
| `SE01`   | Administração de requests por nome ou usuário. |
| `SE03`   | Transport Organizer Tools. |
| `SE09`   | Organização das change requests em desenvolvimento. |
| `STMS`   | Gerenciamento e importação dos transportes entre ambientes SAP. |

---

## 🔄 Fluxo Geral de um Transport Request

O fluxo padrão de um Transport Request no SAP segue geralmente os seguintes passos:

1. **Criação da solicitação** (request), seja Workbench ou Customizing.
2. **Atribuição dos objetos modificados/criados** à request.
3. **Liberação da task** (subnível da request).
4. **Liberação da request principal**.
5. **Importação nos ambientes subsequentes** (QA, Produção), via **STMS**.

---

## 🚚 STMS – SAP Transport Management System

A **STMS** é a transação responsável pela **importação dos transportes** entre os ambientes SAP. Após a **liberação (release)** de uma request no ambiente de desenvolvimento, ela se torna visível na STMS para ser importada nos demais ambientes (como QA e PRD).

### Funcionalidades da STMS:

- Visualização da **fila de importação** por sistema.
- Execução de **importações individuais ou em massa**.
- Verificação do **histórico de transportes**.
- **Configuração de rotas** de transporte entre os ambientes SAP.
- **Logs detalhados** de sucesso ou erro após a importação.

---

## 📝 Observações

Este repositório tem como objetivo fornecer dicas rápidas e diretas para facilitar o entendimento e uso das transport requests no ambiente SAP.  
Ideal para iniciantes ou profissionais que desejam uma referência prática.

---

## 📬 Contribuições

Fique à vontade para contribuir com melhorias, correções ou sugestões para este guia!



