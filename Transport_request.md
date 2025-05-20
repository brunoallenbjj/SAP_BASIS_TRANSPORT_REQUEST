# 📦 Como Criar e Gerenciar Transport Requests no SAP

Este documento explica como criar, liberar e acompanhar **Solicitações de Transporte (Transport Requests)** no SAP, fundamentais para mover alterações entre ambientes (ex: DEV → QAS → PRD).

---

## 🛠️ 1. Criação Automática de Request (ao modificar objetos)

A maioria das Transport Requests é criada automaticamente ao alterar ou criar objetos no SAP, como:

* Programas ABAP (`SE80`, `SE38`)
* Configurações via SPRO
* Objetos do dicionário (`SE11`)
* Funções e classes (`SE37`, `SE24`)

### Exemplo: Criar um programa ABAP

1. Vá para `SE80` ou `SE38`.
2. Crie ou altere um programa.
3. Ao salvar, o SAP pedirá para atribuir a uma request.
4. Clique em **"Criar pedido"**, preencha a descrição e confirme.
5. O SAP criará uma Workbench Request com um número como `DEVK900123`.

---

## 🧾 2. Criação Manual de Transport Request

### Usando SE09 ou SE10

| Transação | Tipo de Request                                  |
| --------- | ------------------------------------------------ |
| `SE09`    | Workbench (programas, tabelas, objetos técnicos) |
| `SE10`    | Customizing (parametrizações e configurações)    |

### Passos:

1. Acesse `SE10` (Customizing Request).
2. Clique em **Criar (F8)**.
3. Escolha **Customizing Request**.
4. Preencha:

   * **Descrição**: Ex: "Criação de nova conta contábil"
   * **Responsável**: O seu usuário
   * **Destino**: Mandante ou sistema destino, se aplicável
5. Clique em **Salvar**. O SAP atribui um número ao request (ex: `DEVK900456`).

---

### 🧪 Exemplo: Criar uma Nova Conta Contábil com Request Manual

1. Acesse a transação `FS00`.
2. Clique em **Criar**.
3. Insira o número da nova conta, descrição, grupo de contas, tipo de conta etc.
4. Ao salvar, o SAP solicitará uma Transport Request.
5. Clique em **Atribuir a um pedido existente** ou selecione **Criar novo**.
6. Use a request criada na `SE10` (ou crie uma nova conforme descrito acima).

> 📌 Esse tipo de alteração é considerada **Customizing** e, por isso, deve ser gerenciada em requests do tipo Customizing (`SE10`).

\-----------|---------------------------|
\| `SE09`    | Workbench (programas, tabelas, objetos técnicos) |
\| `SE10`    | Customizing (parametrizações e configurações)    |

### Passos:

1. Acesse `SE09` ou `SE10`.
2. Clique em **Criar (F8)**.
3. Escolha o tipo de request:

   * **Workbench Request** (técnica)
   * **Customizing Request** (parametrizações)
4. Preencha:

   * **Descrição**
   * **Responsável** (usuário atual)
   * **Destino** (se necessário)
5. Clique em **Salvar**.

O SAP atribui um número ao request (ex: `DEVK900456`), que poderá ser utilizado em modificações futuras.

---

## ➕ Como Adicionar Objetos Manualmente a uma Transport Request

Em algumas situações, você pode precisar adicionar objetos técnicos manualmente a uma Transport Request já criada — especialmente ao lidar com cópias, correções ou agrupamentos específicos.

### 🧭 Transações Usadas

* `SE09` ou `SE10` – para localizar e editar a request
* `SE03` – para operações avançadas com objetos
* `R3TR` – tipo de objeto técnico no SAP

### 🔹 Passo a Passo: Adicionar Objetos Manualmente

1. **Acesse a transação `SE09`** (para requests do tipo Workbench) ou `SE10` (para Customizing).
2. Localize sua **request** e dê duplo clique nela.
3. Clique em **"Exibir/Modificar (botão do lápis)"**.
4. Clique com o botão direito sobre o **request principal ou uma subtask** e escolha **"Incluir objetos..."**.
5. Na janela que se abre:

   * **Objeto (ex: R3TR PROG)**: tipo e categoria do objeto

     * Exemplos:

       * `R3TR PROG` – Programa ABAP
       * `R3TR TABL` – Tabela
       * `R3TR CLAS` – Classe
       * `R3TR FUGR` – Grupo de funções
   * **Nome do objeto**: ex: `ZPROGRAMA_EXEMPLO`
6. Confirme com **Enter** e salve.

> 🔍 Se você não souber o tipo do objeto, use a transação `SE03` → *"Object Directory Entry"* para consultá-lo.

### 🧪 Exemplo Prático

Para adicionar um programa Z chamado `Z_MEUPROGRAMA`:

* Objeto: `R3TR PROG`
* Nome: `Z_MEUPROGRAMA`

### ⚠️ Observações Importantes

* Apenas usuários com perfil adequado podem adicionar objetos manualmente.
* Verifique se o objeto já não está atribuído a outro request (use `SE03` → *Search for Objects in Requests*).
* Adicionar manualmente objetos incorretos pode causar erros no transporte.

---

## 📤 3. Liberação da Request (Release)

Antes de transportar para outros ambientes, o request precisa ser liberado:

1. Vá para `SE09` ou `SE10`.
2. Localize sua request.
3. Libere **primeiro as subtasks** (se existirem).
4. Depois, libere o request principal.

🔁 A liberação gera os arquivos de transporte no diretório do sistema e os prepara para importação via STMS.

---

## 🚚 4. Importação no Ambiente de Destino (STMS)

1. Acesse `STMS`.
2. Vá para **Import Overview**.
3. Selecione o ambiente de destino (ex: `QAS`, `PRD`).
4. Clique em **STMS\_IMPORT** para ver os requests disponíveis.
5. Selecione o request e clique em **Importar** (ícone caminhão).

Opcionalmente, você pode:

* Agendar horário de importação
* Ativar modo de teste
* Ignorar logs de importação

---

## 💻 5. Criação de Request via Código ABAP (Avançado)

```abap
DATA: lv_request TYPE trkorr.

CALL FUNCTION 'TR_INSERT_REQUEST_WITH_TASKS'
  EXPORTING
    iv_type   = 'W'    " W = Workbench | C = Customizing
    iv_text   = 'Criação automática via programa'
    iv_target = 'QAS'
  IMPORTING
    ev_request = lv_request.

WRITE: / 'Request criada:', lv_request.
```

> ⚠️ Apenas para usuários com conhecimento técnico e permissões adequadas.

---

## 🧠 Boas Práticas

* Sempre use descrições claras nas requests.
* Organize requests por tema ou projeto.
* Libere apenas quando tiver certeza da conclusão.
* Nunca transporte diretamente para PRD sem testes em QAS.
* Mantenha rastreabilidade entre TRs e os tickets/chamados de negócio.

---

## 🧭 Transações Relacionadas

| Transação               | Descrição                                                     |
| ----------------------- | ------------------------------------------------------------- |
| `STMS`                  | Gerenciar rotas de transporte e visualizar requests pendentes |
| `SE09`                  | Requests de Workbench                                         |
| `SE10`                  | Requests de Customizing                                       |
| `STMS_IMPORT`           | Importação direta de TRs                                      |
| `SCC1`                  | Importar requests de outro mandante                           |
| `TP` (linha de comando) | Executar transporte manualmente via SO                        |
| `OS01`                  | Verificar diretórios de transporte                            |

---

> 📌 Esse documento faz parte do catálogo técnico SAP. Mantenha-o atualizado conforme as diretrizes do seu landscape.
