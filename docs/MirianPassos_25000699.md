# Avaliação — Engenharia de Software
## Sistema Integrado de Gestão de Farmácia — SGF

**Aluno:** Mirian Suelen Passos  
**RA:** 25000699  
**Data:** 25/03/2026

---

## 1. Definição do MVP
Este MVP foca no fluxo crítico de vendas e controle de estoque, garantindo a operação básica do balcão e a saúde financeira da empresa.

---

## 2. Regras de Negócio 
* **RN01 — Saldo Positivo:** Bloqueia venda se o estoque estiver zerado.  
* **RN02 — Venda Nominal:** Venda a prazo exige cliente cadastrado.  
* **RN03 — Baixa Automática:** Toda venda subtrai itens do inventário.  
* **RN04 — Registro de Débito:** Vendas a prazo geram títulos financeiros.  
* **RN05 — Recibo Detalhado:** Toda venda gera um comprovante impresso ou digital.

---

## 5. Casos de Uso (Geral)
![Diagrama Geral](https://github.com/user-attachments/assets/089a1ecd-5ab0-4d70-9f4f-d9073f5acdfb)

---

## 6. Documentação dos Casos de Uso

### UC01 — Cadastrar Cliente
**Ator:** Atendente | **Descrição:** Registro de novos consumidores.  
**Fluxos Alternativos:** FA01 (CPF Duplicado), FA02 (Dados Incompletos).  
**Relacionamentos:** Nenhum.  
![Atividade UC01](https://github.com/user-attachments/assets/65b31677-fbef-4d35-951f-91db5e24c910)

---

### UC02 — Consultar Cliente
**Ator:** Atendente | **Descrição:** Localizar dados de clientes.  
**Exceções:** Cliente não encontrado.  
**Relacionamentos:** Extend: UC10.  
![Atividade UC02]([COLE_AQUI_O_LINK_DA_IMAGEM])

---

### UC03 — Inserir Produto no Catálogo
**Ator:** Gerente | **Descrição:** Cadastro técnico de medicamentos/itens.  
**Exceções:** Código de barras duplicado.  
![Atividade UC03]([COLE_AQUI_O_LINK_DA_IMAGEM])

---

### UC04 — Localizar Produto
**Ator:** Atendente | **Descrição:** Consulta de preço e saldo em estoque.  
![Atividade UC04]([COLE_AQUI_O_LINK_DA_IMAGEM])

---

### UC05 — Registrar Venda
**Ator:** Atendente | **Descrição:** Operação principal de saída de mercadoria.  
**Relacionamentos:** Include: UC07, UC08. Extend: UC06.  
![Atividade UC05]([COLE_AQUI_O_LINK_DA_IMAGEM])

---

### UC06 — Registrar Venda a Prazo
**Ator:** Atendente | **Descrição:** Venda via crediário para clientes cadastrados.  
**Relacionamentos:** Include: UC09.  
![Atividade UC06]([COLE_AQUI_O_LINK_DA_IMAGEM])

---

### UC07 — Atualizar Estoque
**Ator:** Sistema | **Descrição:** Baixa automática de itens no inventário.  
![Atividade UC07]([COLE_AQUI_O_LINK_DA_IMAGEM])

---

### UC08 — Emitir Comprovante
**Ator:** Sistema | **Descrição:** Geração de cupom fiscal ou recibo.  
![Atividade UC08]([COLE_AQUI_O_LINK_DA_IMAGEM])

---

### UC09 — Gerar Conta a Receber
**Ator:** Financeiro | **Descrição:** Lançamento de títulos de parcelamento.  
![Atividade UC09]([COLE_AQUI_O_LINK_DA_IMAGEM])

---

### UC10 — Ver Histórico de Compras
**Ator:** Atendente | **Descrição:** Relatório de consumo por cliente.  
![Atividade UC10]([COLE_AQUI_O_LINK_DA_IMAGEM])
