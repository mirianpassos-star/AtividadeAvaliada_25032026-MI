# Avaliação — Engenharia de Software
## Sistema Integrado de Gestão de Farmácia — MVP Definido pelo Estudante

**Aluno:** Mirian Suelen Passos 
**RA:** 25000699  
**Data:** 25/03/2026

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



# Documentação dos Casos de Uso - MVP Sistema Saúde & Vida

## UC01 — Cadastrar Cliente
**Ator(es):** Atendente  
**Descrição:** Permite cadastrar um novo cliente, adicionando informações básicas para vincular compras futuras.  
**Pré-condições:** Atendente deve estar logado no sistema.  
**Pós-condições:** Cliente cadastrado no banco de dados.

### Fluxo Principal
1. Atendente seleciona “Cadastrar Cliente”.  
2. Sistema solicita dados do cliente (nome, CPF, telefone, endereço).  
3. Atendente preenche e confirma.  
4. Sistema salva o cliente e confirma o cadastro.

### Fluxos Alternativos / Exceções
- **FA01 — Cliente já cadastrado:** Sistema alerta e oferece atualizar cadastro.

### Relacionamentos
- **Incluir:** Nenhum  
- **Estender:** Nenhum

---

## UC02 — Consultar Cliente
**Ator(es):** Atendente, Cliente  
**Descrição:** Permite buscar clientes cadastrados para vincular vendas ou visualizar informações.  
**Pré-condições:** Cliente deve estar cadastrado.  
**Pós-condições:** Informações do cliente exibidas.

### Fluxo Principal
1. Atendente seleciona “Consultar Cliente”.  
2. Sistema solicita critério de busca (nome, CPF).  
3. Atendente insere dados e confirma.  
4. Sistema exibe os resultados.

### Fluxos Alternativos / Exceções
- **FA01 — Cliente não encontrado:** Sistema exibe mensagem “Cliente não encontrado”.

### Relacionamentos
- **Incluir:** Nenhum  
- **Estender:** Consultar Histórico de Compras do Cliente (UC10)

---

## UC03 — Cadastrar Produto
**Ator(es):** Atendente  
**Descrição:** Permite cadastrar produtos na farmácia, incluindo informações de estoque e preço.  
**Pré-condições:** Atendente logado com permissão de gerente.  
**Pós-condições:** Produto cadastrado no sistema.

### Fluxo Principal
1. Atendente seleciona “Cadastrar Produto”.  
2. Sistema solicita dados (nome, código de barras, preço, fabricante, unidade).  
3. Atendente preenche e confirma.  
4. Sistema salva o produto e confirma.

### Fluxos Alternativos / Exceções
- **FA01 — Produto já cadastrado:** Sistema alerta e oferece atualizar dados.

### Relacionamentos
- **Incluir:** Nenhum  
- **Estender:** Nenhum

---

## UC04 — Consultar Produto
**Ator(es):** Atendente  
**Descrição:** Permite localizar produtos para venda ou verificação de estoque.  
**Pré-condições:** Produto cadastrado no sistema.  
**Pós-condições:** Informações do produto exibidas.

### Fluxo Principal
1. Atendente seleciona “Consultar Produto”.  
2. Sistema solicita critério de busca (nome, código, fabricante).  
3. Atendente insere dados e confirma.  
4. Sistema exibe os produtos encontrados.

### Fluxos Alternativos / Exceções
- **FA01 — Produto não encontrado:** Sistema alerta que produto não existe.

### Relacionamentos
- **Incluir:** Nenhum  
- **Estender:** Nenhum

---

## UC05 — Registrar Venda
**Ator(es):** Atendente  
**Descrição:** Permite registrar vendas de produtos a um cliente, atualizando estoque e emitindo comprovante.  
**Pré-condições:** Cliente cadastrado; produtos disponíveis em estoque.  
**Pós-condições:** Venda registrada, estoque atualizado, comprovante emitido.

### Fluxo Principal
1. Atendente seleciona “Registrar Venda”.  
2. Sistema solicita identificação do cliente.  
3. Atendente adiciona produtos à venda.  
4. Sistema verifica estoque (<<include>> Atualizar Estoque).  
5. Sistema calcula total e confirma venda.  
6. Sistema emite comprovante (<<include>> Emitir Comprovante de Venda).

### Fluxos Alternativos / Exceções
- **FA01 — Produto sem estoque:** Sistema alerta e impede inclusão do produto.  
- **FA02 — Venda a prazo:** Sistema direciona para Registrar Venda a Prazo (<<extend>>).

### Relacionamentos
- **Incluir:** Atualizar Estoque (UC7), Emitir Comprovante de Venda (UC8)  
- **Estender:** Registrar Venda a Prazo (UC6)

---

## UC06 — Registrar Venda a Prazo
**Ator(es):** Atendente / Financeiro  
**Descrição:** Registra vendas a prazo, gerando contas a receber automáticas.  
**Pré-condições:** Venda iniciada; cliente cadastrado.  
**Pós-condições:** Conta a receber criada; venda registrada.

### Fluxo Principal
1. Atendente indica que a venda será a prazo.  
2. Sistema solicita vencimento e confirma dados do cliente.  
3. Sistema gera conta a receber (<<include>> Gerar Conta a Receber).  
4. Sistema confirma venda a prazo.

### Fluxos Alternativos / Exceções
- **FA01 — Cliente não cadastrado:** Sistema solicita cadastro antes de prosseguir.

### Relacionamentos
- **Incluir:** Gerar Conta a Receber (UC9)  
- **Estender:** Registro iniciado por Registrar Venda (UC5)

---

## UC07 — Atualizar Estoque
**Ator(es):** Sistema  
**Descrição:** Atualiza estoque automaticamente após venda ou devolução.  
**Pré-condições:** Venda ou devolução registrada.  
**Pós-condições:** Estoque refletindo a operação realizada.

### Fluxo Principal
1. Sistema recebe notificação de venda ou devolução.  
2. Sistema ajusta a quantidade disponível do produto.  
3. Sistema alerta se estoque estiver abaixo do mínimo.

### Fluxos Alternativos / Exceções
- **FA01 — Estoque insuficiente:** Sistema impede finalização da venda.

### Relacionamentos
- **Incluir:** Nenhum  
- **Estender:** Nenhum

---

## UC08 — Emitir Comprovante de Venda
**Ator(es):** Sistema  
**Descrição:** Gera comprovante detalhado da venda para o cliente.  
**Pré-condições:** Venda registrada.  
**Pós-condições:** Comprovante emitido e registrado.

### Fluxo Principal
1. Sistema gera comprovante com cliente, produtos, quantidade e valor.  
2. Atendente entrega comprovante ao cliente.

### Fluxos Alternativos / Exceções
- **FA01 — Falha na impressora:** Sistema oferece salvar em PDF.

### Relacionamentos
- **Incluir:** Nenhum  
- **Estender:** Nenhum

---

## UC09 — Gerar Conta a Receber
**Ator(es):** Sistema / Financeiro  
**Descrição:** Cria registro de contas a receber para vendas a prazo.  
**Pré-condições:** Venda a prazo iniciada.  
**Pós-condições:** Conta a receber registrada com status “Aberta”.

### Fluxo Principal
1. Sistema cria conta com valor, vencimento e cliente.  
2. Sistema registra status inicial como “Aberta”.

### Fluxos Alternativos / Exceções
- **FA01 — Dados incompletos do cliente:** Sistema solicita preenchimento antes de criar conta.

### Relacionamentos
- **Incluir:** Nenhum  
- **Estender:** Nenhum

---

## UC10 — Consultar Histórico de Compras do Cliente
**Ator(es):** Atendente / Cliente  
**Descrição:** Permite visualizar todas as compras realizadas por um cliente.  
**Pré-condições:** Cliente cadastrado.  
**Pós-condições:** Histórico exibido.

### Fluxo Principal
1. Atendente ou cliente seleciona “Histórico de Compras”.  
2. Sistema solicita identificação do cliente.  
3. Sistema exibe lista de todas as compras com detalhes.

### Fluxos Alternativos / Exceções
- **FA01 — Cliente sem compras:** Sistema informa que não há histórico disponível.

### Relacionamentos
- **Incluir:** Nenhum  
- **Estender:** Consultar Cliente (UC2)
  <img width="2392" height="694" alt="image" src="https://github.com/user-attachments/assets/c95bdb37-9857-4a5a-9e17-c4cb75935d58" />
