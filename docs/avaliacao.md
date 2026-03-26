# Avaliação — Engenharia de Software
## Sistema Integrado de Gestão de Farmácia — MVP Definido pelo Estudante

**Aluno:** Preencha aqui  
**RA:** Preencha aqui  
**Data:** Preencha aqui

---

## 1. Definição do MVP
Meu MVP cobre o **processo de venda desde a identificação/cadastro do cliente até a emissão do comprovante**, incluindo:

### Incluído no MVP
- Cadastro e consulta de clientes  
- Cadastro e consulta de produtos  
- Registro de vendas  
- Registro de vendas a prazo  
- Atualização automática de estoque  
- Emissão de comprovante de venda  
- Geração de contas a receber para vendas a prazo  
- Consulta de histórico de compras do cliente  

### Fora do MVP
- Compras a fornecedores  
- Contas a pagar  
- Relatórios estratégicos avançados  
- Gestão completa de usuários e permissões  
- Integração entre múltiplas unidades da farmácia  

### Justificativa
O foco do MVP é permitir que o fluxo de **vendas e clientes** funcione de forma confiável, garantindo atualização de estoque e registro de contas a receber, que são processos críticos para operação da farmácia.

---

## 2. Regras de Negócio (mínimo: 5)

**RN01 — Venda somente com estoque disponível**  
Um produto só pode ser vendido se houver quantidade suficiente em estoque; caso contrário, o sistema impede a venda.

**RN02 — Cadastro de cliente obrigatório para vendas a prazo**  
Todas as vendas a prazo devem estar vinculadas a um cliente cadastrado, permitindo controle de contas a receber.

**RN03 — Atualização automática de estoque**  
O estoque deve ser atualizado automaticamente após qualquer venda, devolução ou reposição.

**RN04 — Registro de contas a receber**  
Vendas a prazo geram automaticamente uma conta a receber com data de vencimento e status (Aberta, Recebida, Atrasada).

**RN05 — Emissão de comprovante de venda**  
Todo registro de venda deve gerar um comprovante detalhado, contendo cliente, produtos, quantidade, preço e valor total.

### Regras de Negócio Extras
**RN06 — Não vender produtos inexistentes**  
Produtos que não estão cadastrados no sistema não podem ser vendidos.

**RN07 — Consulta de produto obrigatória antes da venda**  
O atendente deve consultar o produto no sistema antes de registrar a venda, garantindo informações corretas de preço e estoque.

**RN08 — Histórico de compras do cliente**  
Todas as compras realizadas devem ficar registradas no histórico do cliente, permitindo acompanhamento e análise futura.

**RN09 — Controle de status das contas a receber**  
O sistema deve atualizar automaticamente o status das contas a receber (Aberta, Recebida, Atrasada) conforme pagamentos sejam registrados.

**RN10 — Restrição de acesso por perfil**  
Cada usuário só pode realizar ações de acordo com seu perfil (atendente, gerente, financeiro, administrador), garantindo segurança e organização.

---

## 3. Requisitos Funcionais (mínimo: 8)

**RF01 — Cadastro de clientes**  
O sistema deve permitir cadastrar novos clientes com informações básicas (nome, telefone, endereço).

**RF02 — Consulta de clientes**  
O sistema deve permitir buscar clientes pelo nome ou CPF para vincular vendas.

**RF03 — Cadastro de produtos**  
O sistema deve permitir cadastrar produtos com descrição, preço, unidade de medida e fabricante.

**RF04 — Consulta de produtos**  
O sistema deve permitir pesquisar produtos pelo nome, código de barras ou fabricante.

**RF05 — Registro de vendas**  
O sistema deve permitir registrar vendas de produtos, associando-os a um cliente e atualizando o estoque.

**RF06 — Atualização automática de estoque**  
O sistema deve atualizar automaticamente a quantidade disponível de produtos após cada venda ou devolução.

**RF07 — Registro de vendas a prazo**  
O sistema deve gerar automaticamente contas a receber para vendas realizadas a prazo, com vencimento e status.

**RF08 — Emissão de comprovante de venda**  
O sistema deve emitir um comprovante detalhado para cada venda, contendo cliente, produtos, quantidade, preço e valor total.

---

## 4. Requisitos Não Funcionais (mínimo: 4)

**RNF01 — Usabilidade**  
O sistema deve ter interface simples e intuitiva, permitindo que atendentes cadastrem clientes e realizem vendas com pouca ou nenhuma dificuldade.

**RNF02 — Desempenho**  
O sistema deve processar consultas de produtos e vendas em até 3 segundos para garantir agilidade no atendimento.

**RNF03 — Segurança**  
O sistema deve restringir acesso conforme perfil do usuário, garantindo que cada função só possa ser executada por usuários autorizados.

**RNF04 — Disponibilidade**  
O sistema deve estar disponível para uso durante todo o horário de funcionamento da farmácia, com mínima interrupção.

---

## 5. Casos de Uso (MVP)

### Atores principais
- **Atendente** – realiza vendas e cadastra clientes  
- **Cliente** – pode ser cadastrado e associado às vendas  
- **Sistema** – realiza verificações e atualizações automáticas  
- **Financeiro** – gerencia contas a receber  

### Casos de Uso do MVP (10)
1. Cadastrar Cliente  
2. Consultar Cliente  
3. Cadastrar Produto  
4. Consultar Produto  
5. Registrar Venda  
6. Registrar Venda a Prazo (<<extend>> “Registrar Venda”)  
7. Atualizar Estoque (<<include>> de “Registrar Venda”)  
8. Emitir Comprovante de Venda (<<include>> de “Registrar Venda”)  
9. Gerar Conta a Receber (<<include>> de “Registrar Venda a Prazo”)  
10. Consultar Histórico de Compras do Cliente (<<extend>> “Consultar Cliente”)  

### Relações importantes
- Registrar Venda <<include>> Atualizar Estoque  
- Registrar Venda <<include>> Emitir Comprovante de Venda  
- Registrar Venda a Prazo <<include>> Gerar Conta a Receber  
- Consultar Cliente <<extend>> Consultar Histórico de Compras do Cliente  
- Registrar Venda <<extend>> Registrar Venda a Prazo (quando o cliente compra a prazo)

---

## 6. Documentação dos Casos de Uso

### UC01 — Cadastrar Cliente
**Ator(es):** Atendente  
**Descrição:** Permite ao atendente cadastrar um novo cliente para associar futuras vendas.  
**Pré-condições:** O atendente deve estar logado no sistema.  
**Pós-condições:** Cliente cadastrado com sucesso no banco de dados.  

**Fluxo Principal:**  
1. Atendente seleciona “Cadastrar Cliente”.  
2. Sistema solicita informações básicas (nome, telefone, CPF).  
3. Atendente preenche e confirma.  
4. Sistema salva os dados e confirma o cadastro.  

**Fluxos Alternativos / Exceções:**  
- FA01 — Cliente já existe: Sistema alerta e sugere atualizar cadastro.  

**Relacionamentos:**  
- Incluir: Nenhum  
- Estender: Nenhum  

---

### UC05 — Registrar Venda
**Ator(es):** Atendente  
**Descrição:** Permite registrar a venda de produtos a um cliente, atualizando estoque e emitindo comprovante.  
**Pré-condições:** Cliente deve estar cadastrado; produtos devem existir no estoque.  
**Pós-condições:** Venda registrada, estoque atualizado, comprovante emitido.  

**Fluxo Principal:**  
1. Atendente seleciona “Registrar Venda”.  
2. Sistema solicita identificação do cliente.  
3. Atendente adiciona produtos à venda.  
4. Sistema verifica estoque (<<include>> Atualizar Estoque).  
5. Sistema calcula total e confirma venda.  
6. Sistema emite comprovante (<<include>> Emitir Comprovante de Venda).  

**Fluxos Alternativos / Exceções:**  
- FA01 — Produto sem estoque: Sistema alerta e impede inclusão do produto.  
- FA02 — Venda a prazo: Sistema direciona para <<extend>> Registrar Venda a Prazo.  

**Relacionamentos:**  
- Incluir: Atualizar Estoque, Emitir Comprovante de Venda  
- Estender: Registrar Venda a Prazo  

---

### UC06 — Registrar Venda a Prazo
**Ator(es):** Atendente / Financeiro  
**Descrição:** Registra vendas a prazo e gera automaticamente a conta a receber.  
**Pré-condições:** Venda deve ser iniciada; cliente cadastrado.  
**Pós-condições:** Conta a receber criada com status “Aberta”.  

**Fluxo Principal:**  
1. Atendente indica que a venda será a prazo.  
2. Sistema solicita vencimento e confirma dados do cliente.  
3. Sistema gera conta a receber (<<include>> Gerar Conta a Receber).  
4. Venda registrada com vínculo a prazo.  

**Fluxos Alternativos / Exceções:**  
- FA01 — Cliente sem cadastro: Sistema solicita cadastro antes de continuar.  

**Relacionamentos:**  
- Incluir: Gerar Conta a Receber  
- Estender: Registro iniciado por “Registrar Venda”  
