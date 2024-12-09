# Desafio E-commerce - DIO

Este README descreve o esquema de banco de dados apresentado no desafio da Digital Innovation One (DIO), voltado para a modelagem de um sistema de e-commerce. Abaixo está a explicação detalhada de cada tabela e seus relacionamentos.

---

## **Descrição Geral do Esquema**

O esquema é composto por diversas tabelas que representam as principais entidades e relações necessárias para gerenciar um sistema de e-commerce. Ele organiza os dados de vendedores, fornecedores, produtos, clientes, pedidos, estoques e formas de pagamento.

---

## **Tabelas e Relacionamentos**

### 1. **Terceiro - vendedor**
- **Descrição**: Representa vendedores terceiros que oferecem produtos na plataforma.
- **Atributos**:
  - `idTerceiro` (INT): Identificador único do vendedor.
  - `Razão Social` (VARCHAR): Nome jurídico do vendedor.
  - `Local` (VARCHAR): Localização do vendedor.
- **Relacionamentos**:
  - Um vendedor pode cadastrar vários produtos na tabela `Produtos por vendedor`.

---

### 2. **Produtos por vendedor**
- **Descrição**: Relaciona produtos oferecidos pelos vendedores terceiros.
- **Atributos**:
  - `Terceiro_idTerceiro` (INT): Chave estrangeira para o vendedor.
  - `Produto_idProduto` (INT): Chave estrangeira para o produto.
  - `Quantidade` (INT): Quantidade do produto disponível.
- **Relacionamentos**:
  - Ligação entre as tabelas `Terceiro - vendedor` e `Produto`.

---

### 3. **Fornecedor**
- **Descrição**: Representa os fornecedores que disponibilizam produtos para os vendedores.
- **Atributos**:
  - `idFornecedor` (INT): Identificador único do fornecedor.
  - `Razão Social` (VARCHAR): Nome jurídico do fornecedor.
  - `CNPJ` (VARCHAR): Cadastro Nacional da Pessoa Jurídica.
- **Relacionamentos**:
  - Um fornecedor pode disponibilizar vários produtos, representados na tabela `Disponibilizando um produto`.

---

### 4. **Disponibilizando um produto**
- **Descrição**: Relaciona produtos disponibilizados pelos fornecedores.
- **Atributos**:
  - `Produto_idProduto` (INT): Chave estrangeira para o produto.
  - `Fornecedor_idFornecedor` (INT): Chave estrangeira para o fornecedor.
- **Relacionamentos**:
  - Conecta as tabelas `Fornecedor` e `Produto`.

---

### 5. **Produto**
- **Descrição**: Armazena informações sobre os produtos disponíveis na plataforma.
- **Atributos**:
  - `idProduto` (INT): Identificador único do produto.
  - `Plataforma` (VARCHAR): Nome da plataforma que gerencia o produto.
  - `Vendedor` (VARCHAR): Nome do vendedor responsável.
  - `Categoria` (VARCHAR): Categoria do produto.
  - `Descrição` (VARCHAR): Descrição detalhada do produto.
  - `Valor` (VARCHAR): Valor do produto.
  - `Pedido_idPedido` (INT): Chave estrangeira para pedidos relacionados.
  - `Pedido_Cliente_idCliente` (INT): Chave estrangeira para o cliente relacionado.
- **Relacionamentos**:
  - Relaciona-se com várias tabelas, como `Estoque_has_Produto`, `Relação de produto/pedido` e `Produtos por vendedor`.

---

### 6. **Cliente**
- **Descrição**: Representa os clientes da plataforma.
- **Atributos**:
  - `idCliente` (INT): Identificador único do cliente.
  - `Nome` (VARCHAR): Nome do cliente.
  - `tipo_cliente` (ENUM): Tipo de cliente (PF ou PJ).
  - `CPF_CNPJ` (VARCHAR): Documento do cliente.
  - `Endereço` (VARCHAR): Endereço do cliente.
- **Relacionamentos**:
  - Um cliente pode ter várias formas de pagamento cadastradas na tabela `Forma de Pagamento` e realizar vários pedidos.

---

### 7. **Forma de Pagamento**
- **Descrição**: Representa as formas de pagamento cadastradas pelos clientes.
- **Atributos**:
  - `idForma de Pagamento` (INT): Identificador único da forma de pagamento.
  - `Descrição` (VARCHAR): Descrição da forma de pagamento.
  - `Cliente_idCliente` (INT): Chave estrangeira para o cliente relacionado.
- **Relacionamentos**:
  - Cada cliente pode ter várias formas de pagamento.

---

### 8. **Pedido**
- **Descrição**: Registra os pedidos realizados pelos clientes.
- **Atributos**:
  - `idPedido` (INT): Identificador único do pedido.
  - `Tempo_carencia` (VARCHAR): Tempo de carência para cancelamento.
  - `Cliente_idCliente` (INT): Chave estrangeira para o cliente que realizou o pedido.
  - `Entregue` (TINYINT): Indica se o pedido foi entregue (1 = sim, 0 = não).
  - `Status_entrega` (VARCHAR): Status atual da entrega.
  - `Cancelado` (TINYINT): Indica se o pedido foi cancelado (1 = sim, 0 = não).
  - `Frete` (FLOAT): Valor do frete.
  - `Codigo_rastreio` (INT): Código de rastreio do pedido.
- **Relacionamentos**:
  - Um pedido pode conter vários produtos, representados na tabela `Relação de produto/pedido`.

---

### 9. **Relação de produto/pedido**
- **Descrição**: Relaciona os produtos com os pedidos realizados.
- **Atributos**:
  - `Produto_idProduto` (INT): Chave estrangeira para o produto.
  - `Pedido_idPedido` (INT): Chave estrangeira para o pedido.
  - `Quantidade` (VARCHAR): Quantidade do produto no pedido.
- **Relacionamentos**:
  - Conecta as tabelas `Produto` e `Pedido`.

---

### 10. **Estoque**
- **Descrição**: Representa os estoques da plataforma.
- **Atributos**:
  - `idEstoque` (INT): Identificador único do estoque.
  - `Local` (VARCHAR): Localização do estoque.
- **Relacionamentos**:
  - Um estoque pode armazenar vários produtos, representados na tabela `Estoque_has_Produto`.

---

### 11. **Estoque_has_Produto**
- **Descrição**: Relaciona produtos armazenados em diferentes estoques.
- **Atributos**:
  - `Estoque_idEstoque` (INT): Chave estrangeira para o estoque.
  - `Produto_idProduto` (INT): Chave estrangeira para o produto.
  - `quantidade` (VARCHAR): Quantidade do produto no estoque.
- **Relacionamentos**:
  - Conecta as tabelas `Estoque` e `Produto`.
