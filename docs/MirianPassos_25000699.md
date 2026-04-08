# Avaliação — Engenharia de Software
## Sistema Integrado de Gestão de Farmácia — MVP Definido pelo Estudante

**Aluno:** Mirian Suelen Passos  
**RA:** 25000699  
**Data:** 25/03/2026

---

## 1. Definição do MVP
Este MVP foca no **fluxo crítico de vendas e controle de estoque**. O objetivo é permitir que a farmácia opere o balcão, gerencie clientes e controle vendas a prazo de forma confiável.

* **Dentro do MVP:** Cadastro de clientes/produtos, registro de vendas (à vista/prazo), baixa automática de estoque, emissão de comprovante e consulta de histórico.
* **Fora do MVP:** Compras de fornecedores, contas a pagar, relatórios de BI e gestão de múltiplas filiais.
* **Justificativa:** Priorizou-se a saúde financeira imediata (vendas e recebíveis) e a integridade do inventário.


## 2. Regras de Negócio 

**RN01 — Saldo Positivo:** Bloqueia venda se o estoque estiver zerado.  
**RN02 — Venda Nominal:** Venda a prazo exige cliente com cadastro ativo.  
**RN03 — Baixa Automática:** Venda confirmada gera decremento imediato no estoque.  
**RN04 — Registro de Débito:** Vendas a prazo criam automaticamente um título no financeiro.  
**RN05 — Recibo Obrigatório:** Toda transação gera um comprovante detalhado.

---

## 3. Requisitos Funcionais 
**RF01** - Cadastrar Cliente | **RF02** - Consultar Cliente | **RF03** - Cadastrar Produto | **RF04** - Consultar Produto | **RF05** - Registrar Venda | **RF06** - Atualizar Estoque | **RF07** - Registrar Venda a Prazo | **RF08** - Emitir Comprovante | **RF09** - Gerar Conta a Receber | **RF10** - Consultar Histórico.

---

## 4. Requisitos Não Funcionais
**RNF01** - Usabilidade (Interface intuitiva) | **RNF02** - Desempenho (< 3s) | **RNF03** - Segurança (Acesso por perfil) | **RNF04** - Disponibilidade (99% em horário comercial).

---

## 5. Casos de Uso (Geral)
<img width="1216" height="477" alt="image" src="https://github.com/user-attachments/assets/089a1ecd-5ab0-4d70-9f4f-d9073f5acdfb" />




---

## 6. Documentação dos Casos de Uso

### UC01 — Cadastrar Cliente
**Ator(es):** Atendente  
**Descrição:** Registro de novos consumidores.  
**Pré-condições:** Sistema logado.  
**Pós-condições:** Cliente salvo no banco.  

**Fluxo Principal:** 1. Atendente solicita CPF. 2. Sistema valida existência. 3. Atendente preenche dados. 4. Sistema confirma.  

**Fluxos Alternativos / Exceções:** - **FA01 — CPF já cadastrado:** Sistema sugere atualizar cadastro.  
- **FA02 — Dados incompletos:** Sistema impede salvamento.  

**Relacionamentos:** - **Include:** Nenhum | **Extend:** Nenhum  

<img width="521" height="896" alt="image" src="https://github.com/user-attachments/assets/65b31677-fbef-4d35-951f-91db5e24c910" />


### UC05 — Registrar Venda
**Ator(es):** Atendente  
**Descrição:** Venda de produtos no balcão.  
**Pré-condições:** Produto em estoque.  
**Pós-condições:** Venda concluída e estoque baixado.  

**Fluxo Principal:** 1. Atendente bipa itens. 2. Sistema soma valores. 3. Seleção do pagamento. 4. Finalização.  

**Fluxos Alternativos / Exceções:** - **FA01 — Estoque Insuficiente:** Alerta visual e bloqueio do item.  
- **FA02 — Cancelamento:** Atendente remove item do carrinho.  

**Relacionamentos:** - **Include:** UC07 (Estoque), UC08 (Comprovante) | **Extend:** UC06 (Venda a Prazo)  

*(Repetir estrutura para os outros 8 casos conforme os modelos anteriores)*
