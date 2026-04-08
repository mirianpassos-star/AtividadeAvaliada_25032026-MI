# Avaliação — Engenharia de Software
## Sistema Integrado de Gestão de Farmácia — MVP Definido pelo Estudante

**Aluno:** Mirian Suelen Passos  
**RA:** 25000699  
**Data:** 25/03/2026

---

## 1. Definição do MVP
Este MVP foi desenhado para sustentar o **core comercial da farmácia**, focando na agilidade do balcão e no controle de quem consome. O objetivo é que o fluxo de venda, do cadastro à baixa física, seja fluido e sem erros.

### Incluído no MVP
- Gestão de cadastros (Clientes e Itens)
- Interface de consulta rápida de preços e saldos
- Módulo de Frente de Caixa (PDV)
- Fluxo de crediário/vendas a prazo
- Sincronização de inventário pós-venda
- Emissão de recibos de compra
- Controle de títulos a receber (financeiro básico)
- Log de histórico de compras por CPF

---

## 2. Regras de Negócio 

**RN01 — Saldo Positivo:** O sistema bloqueia a inserção de produtos no carrinho se o estoque físico constar como zerado.
**RN02 — Venda Nominal:** Para processar vendas a prazo, o vínculo com um cliente já cadastrado é pré-requisito obrigatório.
**RN03 — Baixa Automática:** Toda conclusão de venda gera um gatilho imediato de subtração no saldo do inventário.
**RN04 — Registro de Débito:** Vendas a prazo alimentam automaticamente o módulo de "Contas a Receber".
**RN05 — Recibo Detalhado:** Nenhuma venda é encerrada sem a geração de um comprovante listando itens e total.

---

## 3. Requisitos Funcionais 
**RF01 — Cadastro de Clientes:** Interface para registrar nome, contato e endereço de novos usuários.
**RF02 — Busca de Clientes:** Localização de perfis por nome ou documento (CPF).
**RF03 — Gestão de Produtos:** Cadastro técnico de itens (fabricante, preço, unidade).
**RF04 — Consulta de Itens:** Pesquisa ágil via código de barras ou descrição parcial.
**RF05 — Terminal de Vendas:** Registro de itens selecionados e finalização do carrinho.

---

## 4. Requisitos Não Funcionais
**RNF01 — Usabilidade:** Interface intuitiva para baixa curva de aprendizado.
**RNF02 — Desempenho:** Resposta das consultas e processamento em até 3 segundos.
**RNF03 — Segurança:** Restrição de acesso por perfil (Atendente, Gerente, Financeiro).

---

## 5. Casos de Uso (MVP)

### Atores principais
- **Atendente:** Realiza vendas e cadastros.
- **Financeiro:** Gerencia os títulos de vendas a prazo.
- **Sistema:** Executa processamentos automáticos.

---

## 6. Documentação Detalhada dos Casos de Uso

### UC01 — Cadastrar Cliente
**Ator:** Atendente  
**Descrição:** Permite incluir novos clientes para viabilizar histórico e vendas a prazo.  
**Fluxo Principal:** 1. Solicitar dados (CPF, Nome, Telefone). 
2. Sistema valida CPF. 
3. Atendente preenche e salva.

**Fluxos Alternativos / Exceções:** - **FA01 — CPF já cadastrado:** O sistema alerta que o registro existe e oferece a opção de edição.  
- **FA02 — CPF Inválido:** O sistema impede o salvamento e solicita correção do número.

**Relacionamentos:** - **Incluir:** Nenhum  
- **Estender:** Nenhum

---

### UC05 — Registrar Venda
**Ator:** Atendente  
**Descrição:** Registro de saída de mercadorias no balcão.  
**Fluxo Principal:** 1. Atendente inicia venda. 
2. Sistema solicita identificação (opcional para à vista). 
3. Inserção de itens. 
4. Fechamento e escolha do pagamento.

**Fluxos Alternativos / Exceções:** - **FA01 — Estoque Insuficiente:** O sistema gera alerta visual e impede a adição do item (RN01).  
- **FA02 — Cancelamento de Item:** Atendente remove item antes de fechar o total.

**Relacionamentos:** - **Incluir:** UC07 (Atualizar Estoque), UC08 (Emitir Comprovante).  
- **Estender:** UC06 (Registrar Venda a Prazo).

---

### UC06 — Registrar Venda a Prazo
**Ator:** Atendente / Financeiro  
**Descrição:** Processa vendas que geram dívida para o cliente.

**Fluxos Alternativos / Exceções:** - **FA01 — Cliente não identificado:** O sistema exige a execução do UC02/UC01 para prosseguir.  
- **FA02 — Cliente com pendências:** O sistema alerta sobre débitos atrasados antes de autorizar nova venda.

**Relacionamentos:** - **Incluir:** UC09 (Gerar Conta a Receber).  
- **Estender:** Extensão do UC05.

---

### UC07 — Atualizar Estoque
**Ator:** Sistema  
**Descrição:** Subtração automática das quantidades após a venda.

**Fluxos Alternativos / Exceções:** - **FA01 — Erro de comunicação com Banco de Dados:** O sistema armazena a transação em log local para sincronização posterior.

**Relacionamentos:** - **Incluir:** Nenhum.  
- **Estender:** Nenhum (Incluso no UC05).

---

### UC08 — Emitir Comprovante
**Ator:** Sistema  
**Descrição:** Impressão ou geração de PDF do resumo da venda.

**Fluxos Alternativos / Exceções:** - **FA01 — Falha na Impressora:** O sistema oferece a opção de envio do comprovante por e-mail ou WhatsApp.

**Relacionamentos:** - **Incluir:** Nenhum.  
- **Estender:** Nenhum.

---

### UC10 — Consultar Histórico de Compras
**Ator:** Atendente / Cliente  
**Descrição:** Exibe todas as compras vinculadas a um CPF específico.

**Fluxos Alternativos / Exceções:** - **FA01 — Cliente sem registros:** Sistema exibe mensagem informando que não há compras para o CPF informado.

**Relacionamentos:** - **Incluir:** Nenhum.  
- **Estender:** Extensão do UC02 (Consultar Cliente).

  <img width="2410" height="480" alt="image" src="https://github.com/user-attachments/assets/d9a89c58-1763-4143-847d-e4e3fa4cb832" />

