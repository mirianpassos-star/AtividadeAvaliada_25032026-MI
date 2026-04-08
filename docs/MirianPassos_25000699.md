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
###  Registrar Venda
**Ator(es):** Atendente  
**Descrição:** Processo principal de bipagem de itens, conferência de estoque e recebimento de valores no balcão.  
**Pré-condições:** Atendente logado no sistema; Produtos com saldo positivo no inventário.  
**Pós-condições:** Venda registrada no banco de dados; Estoque atualizado; Comprovante emitido.  

#### Fluxo Principal
1. O Atendente inicia o terminal de vendas (PDV).
2. O Atendente insere os produtos através de código de barras ou busca nominal.
3. O Sistema valida o preço unitário e a disponibilidade física de cada item.
4. O Atendente seleciona a forma de pagamento (Dinheiro, Cartão ou Prazo).
5. O Sistema finaliza a transação e dispara as rotinas de baixa e impressão.

#### Fluxos Alternativos / Exceções
* **FA01 — Estoque Insuficiente:** O sistema identifica saldo zerado, emite um alerta sonoro/visual e impede a inclusão do item no carrinho.
* **FA02 — Cancelamento de Item:** O atendente remove um produto da lista de compras a pedido do cliente antes do fechamento total.

#### Relacionamentos
* **Include:** UC07 (Atualizar Estoque), UC08 (Emitir Comprovante).
* **Extend:** UC06 (Registrar Venda a Prazo).

![Diagrama Geral](https://github.com/user-attachments/assets/089a1ecd-5ab0-4d70-9f4f-d9073f5acdfb)

---

## 6. Documentação dos Casos de Uso

### UC01 — Cadastrar Cliente
**Ator(es):** Atendente  
**Descrição:** Registro de novos consumidores.  
**Pré-condições:** Sistema logado.  
**Pós-condições:** Cliente salvo no banco.  

**Fluxo Principal:** 1. Atendente solicita CPF. 2. Sistema valida existência. 3. Atendente preenche dados. 4. Sistema confirma.  
**Fluxos Alternativos / Exceções:** FA01 — CPF já cadastrado; FA02 — Dados incompletos.  
**Relacionamentos:** Include: Nenhum | Extend: Nenhum
<img width="954" height="559" alt="image" src="https://github.com/user-attachments/assets/8c2835ab-9846-4370-baee-3c41d099b00b" />

---

### UC02 — Consultar Cliente
**Ator(es):** Atendente  
**Descrição:** Busca de dados de clientes cadastrados.  
**Fluxo Principal:** 1. Informar Nome/CPF. 2. Sistema busca no banco. 3. Exibir dados.  
**Exceções:** FA01 — Cliente não encontrado.  
**Relacionamentos:** Extend: UC10 (Histórico).
<img width="736" height="387" alt="image" src="https://github.com/user-attachments/assets/4a825a56-f725-4227-b67a-184d11581714" />


---

### UC03 — Inserir Produto no Catálogo
**Ator(es):** Atendente (Gerente)  
**Descrição:** Inclusão de novos itens no catálogo.  
**Fluxo Principal:** 1. Informar Código/Nome. 2. Definir Preço e Estoque inicial. 3. Salvar.  
**Exceções:** FA01 — Produto já existente.


<img width="610" height="367" alt="image" src="https://github.com/user-attachments/assets/c04b82af-055e-44a2-9610-fb13c9fc48d0" />

---


### UC04 — Consultar Produto
**Ator(es):** Atendente  
**Descrição:** Verificação de preço e saldo.  
**Fluxo Principal:** 1. Bipar produto. 2. Sistema exibe informações.

<img width="413" height="273" alt="image" src="https://github.com/user-attachments/assets/6ac97fed-779d-491b-bb7f-d3eccfd67343" />

### UC05 — Registrar Venda
**Ator(es):** Atendente  
**Descrição:** Venda de produtos no balcão.  
**Pré-condições:** Produto em estoque.  
**Fluxo Principal:** 1. Bipar itens. 2. Somar valores. 3. Selecionar pagamento. 4. Finalizar.  
**Exceções:** FA01 — Estoque insuficiente.  
**Relacionamentos:** Include: UC07, UC08 | Extend: UC06.

<img width="672" height="749" alt="image" src="https://github.com/user-attachments/assets/17a0bb71-8add-4813-a6e0-a9893140d2c6" />


---

### UC06 — Registrar Venda a Prazo
**Ator(es):** Atendente / Financeiro  
**Descrição:** Venda via crediário da loja.  
**Fluxo Principal:** 1. Identificar cliente. 2. Escolher parcelas. 3. Confirmar.  
**Relacionamentos:** Include: UC09 | Extend: UC05. 
<img width="741" height="441" alt="image" src="https://github.com/user-attachments/assets/5b04f900-2bd4-4ccd-ba29-ee2c95bab14a" />


---

### UC07 — Atualizar Estoque
**Ator(es):** Sistema  
**Descrição:** Baixa automática após venda.  
**Fluxo Principal:** 1. Receber itens da venda. 2. Subtrair do banco. 3. Confirmar baixa.

<img width="253" height="351" alt="image" src="https://github.com/user-attachments/assets/153c95fb-5860-4695-93ce-483992dbc39e" />


---

### UC08 — Emitir Comprovante
**Ator(es):** Sistema  
**Descrição:** Geração do cupom de venda.  
**Fluxo Principal:** 1. Coletar dados da venda. 2. Gerar layout. 3. Imprimir ou gerar PDF.
<img width="432" height="266" alt="image" src="https://github.com/user-attachments/assets/4dcb7c63-3f2f-41b3-b971-0f996e2487d7" />


---

### UC09 — Gerar Conta a Receber
**Ator(es):** Sistema / Financeiro  
**Descrição:** Lançamento de títulos no financeiro.  
**Fluxo Principal:** 1. Receber dados do UC06. 2. Agendar vencimentos. 3. Salvar título.

<img width="432" height="381" alt="image" src="https://github.com/user-attachments/assets/70037214-6317-4685-8977-ddc1cbe06b66" />


---

### UC10 — Ver Histórico de Compras
**Ator(es):** Atendente  
**Descrição:** Consulta de transações passadas do cliente.  
**Fluxo Principal:** 1. Consultar Cliente (UC02). 2. Listar compras vinculadas.  
**Relacionamentos:** Extend: UC02.
<img width="675" height="391" alt="image" src="https://github.com/user-attachments/assets/6c3c5f24-a8b2-4e63-8192-85f3cefe8fcf" />

