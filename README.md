# Desafio de Projeto: Refinando um Projeto Conceitual de Banco de Dados – E-COMMERCE

---

<img width="794" height="864" alt="Screenshot_20250822-155554" src="https://github.com/user-attachments/assets/12026176-212d-4f03-9aef-26f9aabb5131" />

---

**Bootcamp Heineken - Inteligência Artificial Aplicada a Dados com Copilot - ministrado pela DIO.me**

--- 

**O diagrama a seguir mostra as entidade de relacionamento, com todas as Entidades do projeto de Banco de Dados Ecommerce e seus devidos Relacionamentos.**

![Screenshot_20250315-224028](https://github.com/user-attachments/assets/4d5cf73f-fee3-43b4-8937-4fccc41adbae)



A seguir apresento, uma análise detalhada do **diagrama de entidade-relacionamento do ecommerce,** considerando as entidades e atributos descritos: 


## 1. Entidade Fornecedor

## Atributos:

idFornecedor (PK): Identificador único de cada fornecedor.

nome, endereço, contato, email, telefone, dataFor: Informações básicas e de contato, além de uma data (possivelmente data de cadastro ou início da relação).


## Papel no sistema:

Fornece os produtos que serão ofertados no ecommerce.

Relaciona-se com as entidades Produto e Estoque (através de chaves estrangeiras), garantindo que cada produto e a respectiva disponibilidade em estoque possam ser associados a um fornecedor específico.


## 2. Entidade Produto

## Atributos:

idProduto (PK): Identificador único do produto.

nome, descrição, preço, dataProd: Informações essenciais sobre o produto, incluindo detalhes e data de inclusão ou fabricação.

idFornecedor (FK): Liga o produto ao seu fornecedor, indicando de onde o produto vem.


## Papel no sistema:

Representa os itens que serão comercializados.

Cada produto está vinculado a um fornecedor, o que facilita a gestão de informações como reposição, qualidade e procedência.



## 3. Entidade Estoque

## Atributos:

idEstoque (PK): Identificador único do registro de estoque.

quantidade, localizacao, dataEsto: Informam a quantidade disponível, o local onde o estoque está armazenado e a data de registro ou atualização do estoque.

idProduto (FK) e idFornecedor (FK): Relacionam o registro de estoque a um produto específico e, novamente, ao fornecedor, o que pode ser útil para casos em que o mesmo produto esteja disponível em diferentes locais ou sob diferentes condições fornecidas por fornecedores distintos.


## Papel no sistema:

Permite o controle da disponibilidade dos produtos.

A associação tanto com o produto quanto com o fornecedor garante a rastreabilidade do inventário, possibilitando o gerenciamento de múltiplas fontes ou depósitos.



## 4. Entidade Cliente e Especializações (ClientePF e ClientePJ)

## Cliente:

Atributos:

idCliente (PK): Identificador único do cliente.

nome, email, telefone, endereco, dataCli: Dados básicos de contato e cadastro do cliente.


## Especializações Disjuntas:

**ClientePF (Pessoa Física):**

idCliente (FK): Reutiliza o identificador do cliente.

CPF: Registro único de pessoa física (no contexto brasileiro).


**ClientePJ (Pessoa Jurídica):**

idCliente (FK): Reutiliza o identificador do cliente.

CNPJ, razaoSocial: Dados específicos para empresas ou organizações.



## Papel no sistema:

A especialização disjunta garante que cada cliente seja categorizado exclusivamente como pessoa física ou jurídica, permitindo regras de negócio diferenciadas (como tratamentos fiscais, forma de pagamento, entre outros).



## 5. Entidade Pedido

Atributos:

idPedido (PK): Identificador único do pedido.

data, status, valorFrete, canceladoFlag: Informações referentes à criação, andamento, custos de frete e flag de cancelamento do pedido.

idCliente (FK): Associa o pedido a um cliente específico.


## Papel no sistema:

Representa a solicitação de compra realizada pelo cliente.

Conecta o cliente aos produtos adquiridos, servindo como base para as entidades relacionadas (itemPedido, Entrega e Pagamento).


## 6. Entidade itemPedido

## Atributos:

idItemPedido (PK): Identificador único do item dentro de um pedido.

quantidade, precoVenda: Especificam a quantidade de determinado produto e o preço praticado na venda.

idPedido (FK): Relaciona o item ao pedido que o contém.

idProduto (FK): Indica qual produto foi vendido.

idEstoque (FK): Possibilita rastrear de qual registro de estoque o produto foi retirado.


## Papel no sistema:

Resolve a relação muitos-para-muitos entre Pedido e Produto (um pedido pode conter vários produtos e um mesmo produto pode estar em diferentes pedidos).

Permite detalhar cada item de um pedido, garantindo a rastreabilidade tanto do produto quanto do estoque de onde ele foi retirado.



## 7. Entidade Entrega

## Atributos:

idEntrega (PK): Identificador único da entrega.

statusEntrega, codigoRastreio, dataEntr: Detalham o status da entrega, o código para rastreamento e a data de entrega.

idPedido (FK): Liga a entrega ao pedido correspondente.


## Papel no sistema:

Monitora e registra o processo logístico de envio do pedido, desde o despacho até a confirmação de entrega.



## 8. Entidade Pagamento

## Atributos:

idPagamento (PK): Identificador único do pagamento.

tipoPagamento, detalhes, dataPag: Informações sobre a forma de pagamento (cartão, boleto, etc.), detalhes adicionais (como parcelas ou códigos de transação) e a data do pagamento.

idCliente (FK) e idPedido (FK): Relacionam o pagamento tanto ao cliente que realizou a transação quanto ao pedido que está sendo quitado.


## Papel no sistema:

Registra as transações financeiras associadas aos pedidos, permitindo o controle e a conciliação dos pagamentos realizados pelos clientes.


## Relações Entre as Entidades

## Fornecedor – Produto:

Cada produto está associado a um único fornecedor, mas um fornecedor pode oferecer diversos produtos. Essa relação garante a origem e a responsabilidade de cada produto.


## Produto – Estoque:

Um produto pode estar presente em vários registros de estoque (por exemplo, em diferentes locais ou depósitos), e cada registro de estoque está vinculado a um produto específico.


## Cliente – Pedido:

Um cliente pode realizar múltiplos pedidos, mas cada pedido é feito por um único cliente. Isso assegura o acompanhamento do histórico de compras e fidelidade do cliente.


## Pedido – itemPedido:

A entidade itemPedido atua como uma tabela de ligação entre Pedido e Produto, permitindo a inclusão de informações específicas (quantidade, preço de venda e referência ao estoque) para cada item do pedido.


## Pedido – Entrega e Pagamento:

Cada pedido possui registros de entrega e pagamento associados, permitindo rastrear o status logístico e financeiro de cada transação.


## Especialização ClientePF/ClientePJ:

O modelo de especialização disjunta assegura que cada cliente seja classificado exclusivamente como pessoa física ou jurídica, o que facilita a aplicação de regras diferenciadas e o tratamento de dados específicos (como CPF para pessoas físicas e CNPJ/razão social para pessoas jurídicas).



## Observações Gerais

## Integridade Referencial:

As chaves primárias (PK) e estrangeiras (FK) são fundamentais para manter a integridade dos dados, assegurando que os relacionamentos entre entidades (como fornecedor com produto ou pedido com cliente) estejam sempre consistentes.


## Rastreabilidade e Controle:

A inclusão de campos de data (dataFor, dataProd, dataEsto, dataCli, dataPag, dataEntr) possibilita o monitoramento temporal das operações – desde o cadastro de fornecedores e produtos até a realização de pedidos, entregas e pagamentos.


## Especialização e Regras de Negócio:

A distinção entre ClientePF e ClientePJ permite a aplicação de regras e políticas específicas para diferentes tipos de clientes, o que pode ser crucial para estratégias de marketing, tributação e relacionamento.


## Gerenciamento de Estoque e Logística:

Ao relacionar itens do pedido com registros específicos de estoque (via idEstoque), o sistema pode acompanhar a origem do produto, facilitando a reposição e a gestão de inventário em múltiplas localizações.


## Modularidade:

Esse diagrama evidencia uma estrutura modular e bem definida, na qual cada entidade cumpre um papel específico dentro do processo de venda online, contribuindo para um sistema robusto e escalável.


Esta modelagem ER contempla os principais aspectos de um ecommerce, desde a aquisição dos produtos junto aos fornecedores até a entrega e o pagamento final pelo cliente.

Cada entidade foi definida com atributos específicos que, combinados, possibilitam um gerenciamento completo do ciclo de vida de uma venda, garantindo rastreabilidade, integridade dos dados e suporte a operações complexas do negócio.


