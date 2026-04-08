# Avaliação — Engenharia de Software
## Sistema Integrado de Gestão de Farmácia — Saúde & Vida

**Aluno:** Mirian Suelen Passos  
**RA:** 25000699  
**Data:** 25/03/2026

---

## 1. Definição do MVP
Este MVP foca no fluxo crítico de vendas e controle de estoque, garantindo a operação básica do balcão e a saúde financeira da empresa Saúde & Vida.

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
**Descrição:** Registro de novos consumidores para permitir histórico e vendas a prazo.  
**Fluxo Principal:** 1. Solicitar CPF; 2. Preencher dados pessoais; 3. Validar endereço; 4. Salvar registro.  
**Fluxos Alternativos / Exceções:** * **FA01 — CPF já cadastrado:** Sistema alerta e sugere atualização de dados.  
* **FA02 — Dados obrigatórios ausentes:** Sistema impede o salvamento até preenchimento total.  
**Relacionamentos:** * **Incluir:** Nenhum  
* **Estender:** UC05 (Registro de Venda)  
![Atividade UC01](https://github.com/user-attachments/assets/8c2835ab-9846-4370-baee-3c41d099b00b)

---

### UC02 — Consultar Cliente
**Ator:** Atendente  
**Descrição:** Busca por dados de clientes no banco centralizado.  
**Fluxo Principal:** 1. Informar CPF ou Nome; 2. Sistema retorna ficha do cliente.  
**Fluxos Alternativos / Exceções:** * **FA01 — Cliente não encontrado:** Sistema oferece opção de novo cadastro.  
**Relacionamentos:** * **Incluir:** Nenhum  
* **Estender:** UC10 (Histórico de Compras)  
![Atividade UC02](https://github.com/user-attachments/assets/4a825a56-f725-4227-b67a-184d11581714)

---

### UC03 — Inserir Produto no Catálogo
**Ator:** Gerente  
**Descrição:** Cadastro de novos produtos, fabricantes e preços de lista.  
**Fluxo Principal:** 1. Inserir dados técnicos; 2. Definir margem de lucro; 3. Salvar no catálogo global.  
**Fluxos Alternativos / Exceções:** * **FA01 — Código EAN Inválido:** Sistema solicita correção do código de barras.  
**Relacionamentos:** * **Incluir:** Nenhum  
* **Estender:** Nenhum  
![Atividade UC03](https://github.com/user-attachments/assets/c04b82af-055e-44a2-9610-fb13c9fc48d0)

---

### UC04 — Consultar Produto
**Ator:** Atendente  
**Descrição:** Verificação de preço e disponibilidade de estoque.  
**Fluxo Principal:** 1. Bipar produto; 2. Visualizar preço e saldo da unidade.  
**Fluxos Alternativos / Exceções:** * **FA01 — Produto sem saldo:** Sistema mostra estoque em unidades vizinhas.  
**Relacionamentos:** * **Incluir:** Nenhum  
* **Estender:** Nenhum  
![Atividade UC04](https://github.com/user-attachments/assets/6ac97fed-779d-491b-bb7f-d3eccfd67343)

---

### UC05 — Registrar Venda
**Ator:** Atendente / Farmacêutico  
**Descrição:** Processo de venda no PDV (Ponto de Venda).  
**Fluxo Principal:** 1. Bipar itens; 2. Somar subtotal; 3. Receber pagamento; 4. Finalizar venda.  
**Fluxos Alternativos / Exceções:** * **FA01 — Medicamento Controlado:** Exige login do Farmacêutico para validar receita.  
* **FA02 — Estoque Insuficiente:** Sistema bloqueia a inclusão do item.  
**Relacionamentos:** * **Incluir:** UC07 (Atualizar Estoque), UC08 (Emitir Comprovante)  
* **Estender:** UC06 (Venda a Prazo), UC01 (Cadastrar Cliente)  
![Atividade UC05](https://github.com/user-attachments/assets/17a0bb71-8add-4813-a6e0-a9893140d2c6)

---

### UC06 — Registrar Venda a Prazo
**Ator:** Atendente  
**Descrição:** Venda com registro de débito em conta para clientes conveniados.  
**Fluxo Principal:** 1. Identificar cliente; 2. Selecionar parcelamento; 3. Confirmar débito.  
**Fluxos Alternativos / Exceções:** * **FA01 — Cliente Inadimplente:** Sistema bloqueia venda a prazo por atrasos anteriores.  
**Relacionamentos:** * **Incluir:** UC09 (Gerar Conta a Receber)  
* **Estender:** UC05 (Registrar Venda)  
![Atividade UC06](https://github.com/user-attachments/assets/5b04f900-2bd4-4ccd-ba29-ee2c95bab14a)

---

### UC07 — Atualizar Estoque
**Ator:** Sistema  
**Descrição:** Atualização automática das quantidades físicas.  
**Fluxo Principal:** 1. Identificar itens vendidos; 2. Abater saldo no banco de dados.  
**Fluxos Alternativos / Exceções:** * **FA01 — Estoque Negativo:** Sistema gera log de erro para auditoria do gerente.  
**Relacionamentos:** * **Incluir:** Nenhum (É incluído pelo UC05)  
* **Estender:** Nenhum  
![Atividade UC07](https://github.com/user-attachments/assets/153c95fb-5860-4695-93ce-483992dbc39e)

---

### UC08 — Emitir Comprovante
**Ator:** Sistema  
**Descrição:** Impressão de cupom detalhado da operação.  
**Fluxo Principal:** 1. Coletar dados da transação; 2. Enviar para impressora fiscal.  
**Fluxos Alternativos / Exceções:** * **FA01 — Erro de Impressora:** Sistema permite salvar em PDF ou reenviar para outra máquina.  
**Relacionamentos:** * **Incluir:** Nenhum (É incluído pelo UC05)  
* **Estender:** Nenhum  
![Atividade UC08](https://github.com/user-attachments/assets/4dcb7c63-3f2f-41b3-b971-0f996e2487d7)

---

### UC09 — Gerar Conta a Receber
**Ator:** Sistema / Financeiro  
**Descrição:** Lançamento de títulos no módulo financeiro da Saúde & Vida.  
**Fluxo Principal:** 1. Receber dados da venda a prazo; 2. Agendar vencimentos; 3. Salvar título.  
**Fluxos Alternativos / Exceções:** * **FA01 — Falha na Integração Financeira:** Sistema armazena localmente e tenta reenvio.  
**Relacionamentos:** * **Incluir:** Nenhum (É incluído pelo UC06)  
* **Estender:** Nenhum  
![Atividade UC09](https://github.com/user-attachments/assets/70037214-6317-4685-8977-ddc1cbe06b66)

---

### UC10 — Ver Histórico de Compras
**Ator:** Atendente / Gerente  
**Descrição:** Consulta detalhada de compras anteriores por CPF.  
**Fluxo Principal:** 1. Selecionar cliente; 2. Listar produtos e datas de compras.  
**Fluxos Alternativos / Exceções:** * **FA01 — Histórico Vazio:** Sistema informa que é a primeira compra do cliente.  
**Relacionamentos:** * **Incluir:** Nenhum  
* **Estender:** UC02 (Consultar Cliente)  
![Atividade UC10](https://github.com/user-attachments/assets/6c3c5f24-a8b2-4e63-8192-85f3cefe8fcf)
