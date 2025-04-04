# SAP_BASIS_TRANSPORT_REQUEST - Dicas simples de utilização


Uma Iransport request nao e nada mais do que um conjunto de alteraçoes/criaçoes de 'funcionalidades' de um ambiente SAP para outro através do que chamamos de um objeto de
transporte. Num objeto de transporte podem conter alterações/criações para tabelas, programas, Jobs e processos.



# Transações utilizadas para Transport de Request

Transação SE01: Transação para administrar requests por nome ou usuário.

Transação SE03: Transport organizer Tools

Transação SE09: é um modo de trabalho para organizar as change requests em desenvolvimento.




# Fluxo de transport de Request

Em geral o fluxo de uma Transport request é o seguinte:

+--------------------------------+
| [Início]                       |
+--------------------------------+
         |
         v
+--------------------------------+
| 1. Desenvolver e testar a      |
|    request no ambiente DEV     |
|    com dados de teste          |
+--------------------------------+
         |
         v
+--------------------------------+
| 2. Liberar a request no        |
|    ambiente DEV para a fila    |
|    de transporte do QAS        |
+--------------------------------+
         |
         v
+--------------------------------+
| 3. Importar a request no       |
|    ambiente QAS                |
+--------------------------------+
         |
         v
+--------------------------------+
| 4. Realizar testes no QAS para |
|    verificar alterações e      |
|    efeitos colaterais          |
+--------------------------------+
         |
         v
+--------------------------------+
| 5. Importar a request no       |
|    ambiente PRD                |
+--------------------------------+
         |
         v
+--------------------------------+
| 6. Liberar as alterações para  |
|    utilização                  |
+--------------------------------+
         |
         v
+--------------------------------+
| [Fim]                          |
+--------------------------------+




