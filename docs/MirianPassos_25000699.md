# Avaliação — Engenharia de Software
## Sistema Integrado de Gestão de Farmácia — Saúde & Vida

**Aluno:** Mirian Suelen Passos  
**RA:** 25000699  
**Data:** 25/03/2026

---

## 1. Definição do MVP
Este MVP foca no fluxo crítico de vendas e controle de estoque, garantindo a integração entre o balcão e o financeiro da farmácia Saúde & Vida.

---

## 2. Regras de Negócio (Mínimo 5)
* **RN01 — Saldo Positivo:** Bloqueia venda se o estoque estiver zerado.  
* **RN02 — Venda Nominal:** Venda a prazo exige cliente com cadastro ativo.  
* **RN03 — Baixa Automática:** Toda venda confirmada subtrai itens do estoque da unidade.  
* **RN04 — Registro de Débito:** Vendas a prazo geram títulos automáticos no Contas a Receber.  
* **RN05 — Retenção de Receita:** Medicamentos controlados exigem validação do Farmacêutico.

---

## 3. Requisitos Funcionais (Mínimo 8)
* **RF01:** Cadastrar e pesquisar produtos por código de barras ou fabricante.
* **RF02:** Registrar vendas à vista e a prazo.
* **RF03:** Efetuar baixa automática de estoque após venda.
* **RF04:** Gerar alerta de estoque abaixo do nível mínimo.
* **RF05:** Cadastrar clientes e vincular ao histórico de compras.
* **RF06:** Registrar contas a pagar (fornecedores) e contas a receber (vendas a prazo).
* **RF07:** Emitir comprovante de venda detalhado.
* **RF08:** Gerar relatórios de produtos mais vendidos e faturamento por unidade.

---

## 4. Requisitos Não Funcionais (Mínimo 4)
* **RNF01:** O sistema deve processar a consulta de estoque em menos de 2 segundos.
* **RNF02:** A interface deve ser intuitiva para atendentes e gerentes.
* **RNF03:** Restrição de acesso baseada em perfis (Atendente, Farmacêutico, Gerente).
* **RNF04:** O sistema deve estar disponível 99% do tempo em horário comercial.

---

## 5. Casos de Uso (Geral)
![Diagrama Geral](https://github.com/user-attachments/assets/089a1ecd-5ab0-4d70-9f4f-d9073f5acdfb)

---

## 6. Documentação dos Casos de Uso

### UC01 — Cadastrar Cliente
**Ator:** Atendente  
**Descrição:** Registro de novos consumidores no banco de dados centralizado.  
**Pré-condição:** Cliente não deve possuir registro prévio com o mesmo CPF.  
**Pós-condição:** Cliente apto a realizar compras nominais e a prazo.  
**Fluxo:** 1. Solicitar CPF; 2. Preencher dados pessoais; 3. Validar endereço; 4. Salvar registro.  
**Relacionamentos:** **Extend:** UC05.  
![Atividade UC01](https://github.com/user-attachments/assets/8c2835ab-9846-4370-baee-3c41d099b00b)

---

### UC02 — Consultar Cliente
**Ator:** Atendente  
**Descrição:** Localizar dados e status financeiro de clientes.  
**Pré-condição:** Sistema com acesso ao banco de dados da matriz.  
**Fluxo:** 1. Informar CPF; 2. Sistema retorna dados e saldo devedor.  
**Relacionamentos:** **Extend:** UC10.  
![Atividade UC02](https://github.com/user-attachments/assets/4a825a56-f725-4227-b67a-184d11581714)

---

### UC03 — Inserir Produto no Catálogo
**Ator:** Gerente  
**Descrição:** Cadastro técnico de novos itens, definindo fabricante e medida.  
**Pós-condição:** Item disponível para pesquisa e venda em todas as unidades.  
![Atividade UC03](https://github.com/user-attachments/assets/c04b82af-055e-44a2-9610-fb13c9fc48d0)

---

### UC04 — Consultar Produto
**Ator:** Atendente / Farmacêutico  
**Descrição:** Verificação de preço de lista e saldo físico na unidade.  
**Fluxo:** 1. Bipar produto; 2. Visualizar estoque da unidade e de unidades próximas.  
![Atividade UC04](https://github.com/user-attachments/assets/6ac97fed-779d-491b-bb7f-d3eccfd67343)

---

### UC05 — Registrar Venda
**Ator:** Atendente / Farmacêutico  
**Descrição:** Operação principal de saída de mercadoria.  
**Pré-condição:** Produto com estoque positivo; Farmacêutico logado se houver receita.  
**Pós-condição:** Venda finalizada e estoque atualizado.  
**Relacionamentos:** **Include:** UC07, UC08 | **Extend:** UC06, UC01.  
![Atividade UC05](https://github.com/user-attachments/assets/17a0bb71-8add-4813-a6e0-a9893140d2c6)

---

### UC06 — Registrar Venda a Prazo
**Ator:** Atendente  
**Descrição:** Venda com pagamento via convênio ou crediário próprio.  
**Pré-condição:** Cliente cadastrado (UC01) e sem restrições financeiras.  
**Relacionamentos:** **Include:** UC09 | **Extend:** UC05.  
![Atividade UC06](https://github.com/user-attachments/assets/5b04f900-2bd4-4ccd-ba29-ee2c95bab14a)

---

### UC07 — Atualizar Estoque
**Ator:** Sistema  
**Descrição:** Baixa automática após a venda confirmada ou reposição via compra.  
**Pós-condição:** Saldo do produto atualizado em tempo real.  
![Atividade UC07](https://github.com/user-attachments/assets/153c95fb-5860-4695-93ce-483992dbc39e)

---

### UC08 — Emitir Comprovante
**Ator:** Sistema  
**Descrição:** Geração de cupom fiscal com descrição do fabricante e valores.  
![Atividade UC08](https://github.com/user-attachments/assets/4dcb7c63-3f2f-41b3-b971-0f996e2487d7)

---

### UC09 — Gerar Conta a Receber
**Ator:** Financeiro / Sistema  
**Descrição:** Lançamento de títulos financeiros com datas de vencimento.  
**Pós-condição:** Título disponível no financeiro com status "Aberta".  
![Atividade UC09](https://github.com/user-attachments/assets/70037214-6317-4685-8977-ddc1cbe06b66)

---

### UC10 — Ver Histórico de Compras
**Ator:** Atendente / Gerente  
**Descrição:** Relatório detalhado de itens adquiridos por um CPF específico.  
**Fluxo:** 1. Consultar Cliente; 2. Selecionar "Histórico"; 3. Filtrar por período.  
**Relacionamentos:** **Extend:** UC02.  
![Atividade UC10](https://github.com/user-attachments/assets/6c3c5f24-a8b2-4e63-8192-85f3cefe8fcf)
