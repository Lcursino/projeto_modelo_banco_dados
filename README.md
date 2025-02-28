![ecommerce](https://github.com/user-attachments/assets/10f7caea-27ea-48e5-973f-7d56f3f1e521)

```markdown
# Modelo de Banco de Dados para E-commerce

## Descrição do Projeto

Este projeto apresenta um modelo de banco de dados relacional para um sistema de e-commerce, projetado para suportar funcionalidades essenciais como gerenciamento de produtos, clientes, pedidos, pagamentos, entregas e vendedores de marketplace. O modelo visa fornecer uma estrutura robusta e escalável para operações de comércio eletrônico, permitindo a gestão eficiente de dados e o suporte a diversas funcionalidades de negócio.

## Diagrama Entidade-Relacionamento (DER)

[Inserir aqui o link ou o caminho para a imagem do seu DER]

## Tabelas e Atributos

### Cliente

- `idCliente` (INT, Chave Primária): Identificador único do cliente.
- `Nome` (VARCHAR(45)): Nome completo do cliente.
- `Tipo` (ENUM('PF', 'PJ')): Indica se o cliente é Pessoa Física ou Pessoa Jurídica.

### ClientePF (Pessoa Física)

- `Cliente_idCliente` (INT, Chave Primária, Chave Estrangeira referenciando Cliente): Identificador do cliente PF.
- `CPF` (CHAR(11)): Cadastro de Pessoa Física.
- `DataNascimento` (DATE): Data de nascimento do cliente.

### ClientePJ (Pessoa Jurídica)

- `Cliente_idCliente` (INT, Chave Primária, Chave Estrangeira referenciando Cliente): Identificador do cliente PJ.
- `CNPJ` (CHAR(14)): Cadastro Nacional da Pessoa Jurídica.
- `RazaoSocial` (VARCHAR(45)): Razão social da empresa.

### Endereco

- `idEndereco` (INT, Chave Primária): Identificador único do endereço.
- `Rua` (VARCHAR(100)): Nome da rua.
- `Numero` (VARCHAR(10)): Número do endereço.
- `Cidade` (VARCHAR(50)): Cidade do endereço.
- `Estado` (VARCHAR(2)): Estado do endereço.
- `CEP` (CHAR(8)): Código de Endereçamento Postal.

### EnderecoPF

- `Endereco_idEndereco` (INT, Chave Primária, Chave Estrangeira referenciando Endereco): Identificador do endereço PF.
- `ClientePF_Cliente_idCliente` (INT, Chave Estrangeira referenciando ClientePF): Identificador do cliente PF associado.

### EnderecoPJ

- `Endereco_idEndereco` (INT, Chave Primária, Chave Estrangeira referenciando Endereco): Identificador do endereço PJ.
- `ClientePJ_Cliente_idCliente` (INT, Chave Estrangeira referenciando ClientePJ): Identificador do cliente PJ associado.

### Pedido

- `idPedido` (INT, Chave Primária): Identificador único do pedido.
- `Cliente_idCliente` (INT, Chave Estrangeira referenciando Cliente): Identificador do cliente que realizou o pedido.
- `Descricao` (LONGTEXT): Descrição detalhada do pedido.
- `Frete` (DECIMAL(10,2)): Valor do frete do pedido.
- `CodigoRastreio` (VARCHAR(20)): Código de rastreamento da entrega.
- `Entrega_idEntrega` (INT, Chave Estrangeira referenciando Entrega): Identificador da entrega associada ao pedido.

### Produto

- `idProduto` (INT, Chave Primária): Identificador único do produto.
- `Categoria` (VARCHAR(45)): Categoria do produto.
- `Descricao` (LONGTEXT): Descrição detalhada do produto.
- `Valor` (DECIMAL(10,2)): Valor do produto.

### ProdutoPedido

- `Produto_idProduto` (INT, Chave Primária, Chave Estrangeira referenciando Produto): Identificador do produto no pedido.
- `Pedido_idPedido` (INT, Chave Primária, Chave Estrangeira referenciando Pedido): Identificador do pedido.
- `Quantidade` (INT): Quantidade do produto no pedido.

### Pagamento

- `idPagamento` (INT, Chave Primária): Identificador único do pagamento.
- `MetodoPagamento` (VARCHAR(45)): Método de pagamento utilizado.
- `DataPagamento` (DATETIME): Data e hora do pagamento.

### PagamentoCliente

- `Pagamento_idPagamento` (INT, Chave Primária, Chave Estrangeira referenciando Pagamento): Identificador do pagamento.
- `Cliente_idCliente` (INT, Chave Primária, Chave Estrangeira referenciando Cliente): Identificador do cliente associado ao pagamento.

### CartaoCredito

- `idCartaoCredito` (INT, Chave Primária): Identificador único do cartão de crédito.
- `Bandeira` (VARCHAR(45)): Bandeira do cartão de crédito.
- `Codigo` (INT): Código do cartão de crédito.
- `Validade` (DATE): Data de validade do cartão de crédito.
- `Pagamento_idPagamento` (INT, Chave Estrangeira referenciando Pagamento): Identificador do pagamento associado.

### Entrega

- `idEntrega` (INT, Chave Primária): Identificador único da entrega.
- `Status` (ENUM('Em processamento', 'Enviado', 'Entregue')): Status da entrega.
- `PrevisaoEntrega` (DATE): Previsão de data de entrega.
- `Empresa` (VARCHAR(45)): Empresa responsável pela entrega.

### Fornecedor

- `idFornecedor` (INT, Chave Primária): Identificador único do fornecedor.
- `RazaoSocial` (VARCHAR(45)): Razão social do fornecedor.
- `CNPJ` (VARCHAR(14)): CNPJ do fornecedor.

### OrigemProduto

- `Produto_idProduto` (INT, Chave Primária, Chave Estrangeira referenciando Produto): Identificador do produto.
- `Fornecedor_idFornecedor` (INT, Chave Primária, Chave Estrangeira referenciando Fornecedor): Identificador do fornecedor do produto.

### ProdutoPorEstoque

- `Produto_idProduto` (INT, Chave Primária, Chave Estrangeira referenciando Produto): Identificador do produto.
- `Estoque_idEstoque` (INT, Chave Primária, Chave Estrangeira referenciando Estoque): Identificador do estoque.
- `Quantidade` (INT): Quantidade do produto em estoque.

### Estoque

- `idEstoque` (INT, Chave Primária): Identificador único do estoque.
- `Local` (VARCHAR(45)): Localização do estoque.

### VendedorMarketplace

- `idVendedor` (INT, Chave Primária): Identificador único do vendedor no marketplace.
- `RazaoSocial` (VARCHAR(45)): Razão social do vendedor.
- `Endereco` (VARCHAR(45)): Endereço do vendedor.

### ProdutosPorVendedor

- `Terceiro_vendedor_idTerceiro_vendedor` (INT, Chave Primária, Chave Estrangeira referenciando VendedorMarketplace): Identificador do vendedor.
- `Produtos_Produto_idProduto` (INT, Chave Primária, Chave Estrangeira referenciando Produto): Identificador do produto vendido pelo vendedor.
- `Quantidade` (INT): Quantidade do produto vendida pelo vendedor.

## Relacionamentos

- **Cliente** 1:N **Pedido**
- **Cliente** 1:N **PagamentoCliente**
- **Cliente** 1:1 **ClientePF** ou **ClientePJ**
- **Endereco** 1:N **EnderecoPF** ou **EnderecoPJ**
- **Pedido** 1:N **ProdutoPedido**
- **Pedido** 1:1 **Entrega**
- **Produto** 1:N **ProdutoPedido**
- **Produto** 1:N **OrigemProduto**
- **Produto** 1:N **ProdutoPorEstoque**
- **Pagamento** 1:N **PagamentoCliente**
- **Pagamento** 1:1 **CartaoCredito**
- **Fornecedor** 1:N **OrigemProduto**
- **Estoque** 1:N **ProdutoPorEstoque**
- **VendedorMarketplace** 1:N **ProdutosPorVendedor**

## Observações

- A modelagem inclui suporte para clientes Pessoa Física (PF) e Pessoa Jurídica (PJ), com tabelas separadas para armazenar informações específicas de cada tipo.
- O sistema permite o gerenciamento de endereços distintos para clientes PF e PJ, mantendo a integridade dos dados.
- A tabela `Pedido` inclui um campo `CodigoRastreio` para rastreamento de entregas, facilitando o acompanhamento dos pedidos pelos clientes.
- A tabela `Entrega` armazena o status, previsão de entrega, e a empresa responsável pela entrega.
