# Boas vindas ao repositório do projeto Store Manager!

Projeto desenvolvido como requisito parcial para conclusão do módulo de Back-end do curso de Desenvolvimento Web da Trybe. Neste projeto, foram criados endpoints de **API RESTful** em **NodeJS** e utilizamos o **MongoDB** como banco de dados. Foram desenvolvidas todas as camadas da API (Models, Services caso necessário, e Controllers). Através dessa aplicação, é possível realizar as operações básicas de um CRUD no banco de dados: Criação, Leitura, Atualização e Exclusão (ou `CRUD`).

- Para **todos os endpoints**:

  - Caso o recurso não seja encontrado, a API retorna o status HTTP adequado com o body `{ message: '<recurso> não encontrado' }`.
  - Em caso de erro, a API retorna o status HTTP adequado com o body `{ err: { message: <mensagem de erro>, code: <código do erro> } }`.
    - Criaram-se padrões de código do erro para toda a aplicação.
  - Em caso de dados inválidos, a API retorna o status HTTP adequado, com o body `{ err: { message: 'Dados inválidos', code: <código do erro> } }`.
  - Todos os retornos de erro seguem o mesmo formato. Para erros que requerem dados adicionais (por exemplo, para informar quais campos estão incorretos) é utilizada a propriedade `data` dentro do objeto `err`.

 
### Todos os endpoints estão no padrão REST

- São usados os verbos HTTP adequados para cada operação.

- As URLs são agrupadas e padronizadas em cada recurso.

- Os endpoints sempre retornem uma resposta, havendo sucesso nas operações ou não.

- Os códigos de status corretos são retornados (recurso criado, erro de validação, autorização, etc).
  
---

# Sumário

- [Habilidades](#habilidades)
- [Data de entrega](#data-de-entrega)
- [Como desenvolver](#como-desenvolver)
- [Conexão com o Banco](#conexão-com-o-banco)
- [Tabelas](#tabelas)
- [Requisitos do projeto](#requisitos-do-projeto)
  - [Lista de requisitos](#lista-de-requisitos)

    `Obrigatórios`
    - [1 - Crie um endpoint para o cadastro de produtos](#1---crie-um-endpoint-para-o-cadastro-de-produtos)
    - [2 - Crie um endpoint para listar os produtos](#2---crie-um-endpoint-para-listar-os-produtos)
    - [3 - Crie um endpoint para atualizar um produto](#3---crie-um-endpoint-para-atualizar-um-produto)
    - [4 - Crie um endpoint para deletar um produto](#4---crie-um-endpoint-para-deletar-um-produto)
    - [5 - Crie um endpoint para cadastrar vendas](#5---crie-um-endpoint-para-cadastrar-vendas)
    - [6 - Crie um endpoint para listar as vendas](#6---crie-um-endpoint-para-listar-as-vendas)
    - [7 - Crie um endpoint para atualizar uma venda](#7---crie-um-endpoint-para-atualizar-uma-venda)
    - [8 - Crie um endpoint para deletar uma venda](#8---crie-um-endpoint-para-deletar-uma-venda)
    - [9 - Atualize a quantidade de produtos](#9---atualize-a-quantidade-de-produtos)
    - [10 - Valide a quantidade de produtos](#10---valide-a-quantidade-de-produtos)

    `Bônus`
    
    - [11 - Escreva testes para seus models](#11---escreva-testes-para-seus-models)
    - [12 - Escreva testes para seus services](#12---escreva-testes-para-seus-services)
    - [13 - Escreva testes para seus controllers](#13---escreva-testes-para-seus-controllers)

---

# Habilidades

Nesse projeto, foram trabalhadas as seguintes habilidades:

- Entendimento do funcionamento da camada de Model;
- Delegação de responsabilidades específicas para essa camada;
- Conexão da aplicação com diferentes bancos de dados;
- Estruturação de uma aplicação em camadas;
- Delegação de responsabilidades específicas para cada parte do app;
- Melhorias de manutenibilidade e reusabilidade do seu código;
- Entendimento e aplicação dos padrões REST;
- Escrita de assinaturas para APIs intuitivas e facilmente entendíveis.

---

## Data de Entrega

  - Foram `3` dias de projeto.
  - Data de entrega para avaliação final do projeto: `21/09/2021 - 14:00h`.

---

### Conexão com o Banco:

A conexão do banco local deverá conter os seguintes parâmetros:

```javascript
const MONGO_DB_URL = 'mongodb://localhost:27017/StoreManager';
const DB_NAME = 'StoreManager';
```

Para o avaliador funcionar altere a conexão do banco para:

```javascript
const MONGO_DB_URL = 'mongodb://mongodb:27017/StoreManager';
const DB_NAME = 'StoreManager';
```

### Tabelas

O banco tem duas tabelas: produtos e vendas

A tabela de produtos tem o seguinte nome: `products`

Os campos da tabela `products` têm esse formato:

```json
{ "name": "Produto Silva", "quantity": 10 }
```

A resposta do insert que é retornada após a criação é parecida com essa:

```json
{ "_id": ObjectId("5f43cbf4c45ff5104986e81d"), "name": "Produto Silva", "quantity": 10 }
```

(O \_id será gerado automaticamente)

A tabela de vendas tem o seguinte nome: `sales`

Os campos da tabela `sales` têm este formato:

```json
{ "itensSold": [{ "productId": "5f43cbf4c45ff5104986e81d", "quantity": 2 }] }
```

A resposta do insert retornada após a criação é parecida com essa:

```json
{
  "_id": ObjectId("5f43cc53c45ff5104986e81e"),
  "itensSold": [{ "productId": "5f43cbf4c45ff5104986e81d", "quantity": 2 }]
}
```

(O \_id será gerado automaticamente)

# Requisitos do projeto

## Lista de requisitos

### 1 - Crie um endpoint para o cadastro de produtos

- O endpoint deve ser acessível através do caminho (`/products`);

- Os produtos enviados devem ser salvos em uma **collection** do MongoDB;

- O endpoint deve receber a seguinte estrutura:

```json
{
  "name": "product_name",
  "quantity": "product_quantity"
}
```

O retorno da API de um produto cadastrado com sucesso deverá ser:

```json
{
  "_id": "5f43a7ca92d58904914656b6",
  "name": "Produto do Batista",
  "quantity": 100
}
```

#### Requisição de Cadastro de Produtos:

O projeto deve rodar na porta `http://localhost:3000`

![Criar produtos](./public/criarProdutos.png)

#### Observações Técnicas:

- `name` deve ser uma _string_ com mais de 5 caracteres e deve ser único;

- `quantity` deve ser um número inteiro maior que 0;

- Cada produto deve ter um id que seja único e gerado no momento em que o recurso for criado. Você pode utilizar o ID gerado pelo MongoDB

- A resposta do endpoint em caso de sucesso deve ser o produto criado.

**O que será verificado:**

- Será validado que não é possível criar um produto com o nome menor que 5 caracteres
  - Se o produto tiver o nome menor que cinco caracteres o resultado retornado deverá ser conforme exibido abaixo, com um status http `422`:

![Nome menor que 5](./public/nomeMenorQue5.png)
(As contrabarras `\` estão escapando as aspas de dentro da string)

- Será validado que não é possível criar um produto com o mesmo nome de outro já existente

  -  Se o produto tiver o mesmo nome o resultado retornado deverá ser conforme exibido abaixo, com status http `422`:

![Mesmo nome](./public/mesmonome.png)

- Será validado que não é possível criar um produto com quantidade menor que zero

    - Se o produto tiver uma quantidade menor que zero o resultado retornado deverá ser conforme exibido abaixo, com status http `422`:

![Menor que 0](./public/menorque0.png)
(As contrabarras `\` estão escapando as aspas de dentro da string)

- Será validado que não é possível criar um produto com quantidade igual a zero

  - Se o produto tiver uma quantidade igual a zero o resultado retornado deverá ser conforme exibido abaixo, com status http `422`:

![Igual a zero](./public/igualazero.png)
(As contrabarras `\` estão escapando as aspas de dentro da string)

- Será validado que não é possível criar um produto com uma string no campo quantidade

  - Se o produto tiver uma quantidade com o valor em string o resultado retornado deverá ser conforme exibido abaixo, com status http `422`:

![Quantidade como string](./public/quantidadecomostring.png)
(As contrabarras `\` estão escapando as aspas de dentro da string)

- Será validado que é possível criar um produto com sucesso

  - Se o produto for cadastrado com sucesso o resultado retornado deverá ser conforme exibido abaixo, com status http `201`:

![Criar produtos](./public/criarProdutos.png)

### 2 - Crie um endpoint para listar os produtos

- O endpoint deve ser acessível através do caminho (`/products`) ou (`/products/:id`);

- Através do caminho `/products`, todos os produtos devem ser retornados;

- Através do caminho `/products/:id`, apenas o produto com o `id` presente na URL deve ser retornado;

**O que será verificado:**

- Será validado que todos produtos estão sendo retornados

  - Se a lista retornar com sucesso, o resultado retornado deverá ser conforme exibido abaixo, com status http `200`:

![Lista de produtos](./public/listadeprodutos.png)

- Será validado que é possível listar um determinado produto

  - Se a lista retornar com sucesso, o resultado retornado deverá ser conforme exibido abaixo, com status http `200`:

![Listar um produto](./public/produtoespecifico.png)

- Será validado que não é possível listar um produto que não existe

  - Se a lista retornar com falha, o resultado retornado deverá ser conforme exibido abaixo, com status http `422`:

![Produto não existe](./public/produtonaoexiste.png)

### 3 - Crie um endpoint para atualizar um produto

- O endpoint deve ser acessível através do caminho (`/products/:id`);

- O corpo da requisição deve seguir a mesma estrutura do método responsável por adicionar um produto;

- Apenas o produto com o `id` presente na URL deve ser atualizado;

**O que será verificado:**

- Será validado que não é possível atualizar um produto com o nome menor que 5 caracteres

  - Se o produto tiver o nome menor que cinco caracteres, o resultado retornado deverá ser conforme exibido abaixo, com status `422`:

![Atualizar com nome menor que cinco](./public/atualizarcomnomemenorque5.png)
(As contrabarras `\` estão escapando as aspas de dentro da string)

- Será validado que não é possível atualizar um produto com quantidade menor que zero

  - Se o produto tiver o quantidade menor que zero, o resultado retornado deverá ser conforme exibido abaixo, com status http `422`:

![Atualizar menor que zero](./public/atualizarmenorque0.png)
(As contrabarras `\` estão escapando as aspas de dentro da string)

- Será validado que não é possível atualizar um produto com quantidade igual a zero

  - Se o produto tiver o quantidade igual a zero, o resultado mostrado deverá ser conforme exibido abaixo, com status http `422`:

![Atualizar igual a zero](./public/atualizarigual0.png)
(As contrabarras `\` estão escapando as aspas de dentro da string)

- Será validado que não é possível atualizar um produto com uma string no campo quantidade

  - Se o produto tiver o quantidade como string, o resultado retornado deverá ser conforme exibido abaixo, com status http `422`:

![Atualizar com string](./public/atualizarcomostring.png)
(As contrabarras `\` estão escapando as aspas de dentro da string)

- Será validado que é possível atualizar um produto com sucesso]**

  - Se o produto atualizado com sucesso, o resultado mostrretornadoado deverá ser conforme exibido abaixo, com status http `200`:

![Atualizado com sucesso](./public/atualizarcomsucesso.png)

### 4 - Crie um endpoint para deletar um produto

- O endpoint deve ser acessível através do caminho (`/products/:id`);

- Apenas o produto com o `id` presente na URL deve ser deletado;

**O que será verificado:**

- Será validado que é possível deletar um produto com sucesso

  - Se o produto deletado com sucesso, o resultado retornado deverá ser conforme exibido abaixo, com status http `200`:

![Deletar um produto](./public/deletarumproduto.png)

- Será validado que não é possível deletar um produto que não existe

  - Se o produto não for deletado com sucesso, o resultado retornado deverá ser esse e com status http `422`:

![Deletar um produto que não existe](./public/deletarumprodutoquenaoexiste.png)

### 5 - Crie um endpoint para cadastrar vendas

- O endpoint deve ser acessível através do caminho (`/sales`);

- As vendas enviadas devem ser salvas em uma `collection` do MongoDB;

- Deve ser possível cadastrar a venda de vários produtos através da uma mesma requisição;

- O endpoint deve receber a seguinte estrutura:

```json
[
  {
  "productId": "product_id",
  "quantity": "product_quantity",
  },
  ...
]
```

O retorno de uma venda cadastrada com sucesso deverá ser:

```json
{
  "_id": "5f43ba333200020b101fe4a0",
  "itensSold": [
    {
      "productId": "5f43ba273200020b101fe49f",
      "quantity": 2
    }
  ]
}
```

#### Observações Técnicas:

- O `productId` devem ser igual ao `id` de um produto anteriormente cadastrado;

- `quantity` deve ser um número inteiro maior que 0;

- Cada venda deve ter um id que seja único e gerado no momento em que o recurso for criado;

- A resposta do endpoint em caso de sucesso deve ser a(s) venda(s) criada(s).

**O que será verificado:**

- Será validado que não é possível cadastrar vendas com quantidade menor que zero

  - Se a venda tiver uma quantidade menor que zero, o resultado retornado deverá ser conforme exibido abaixo, com status http `422`:

![Vendas menor que zero](./public/comprasmenorquezero.png)

- Será validado que não é possível cadastrar vendas com quantidade igual a zero

  - Se a venda tiver uma quantidade igual a zero, o resultado retornado deverá ser conforme exibido abaixo, com status http `422`:

![Vendas igual a zero](./public/comprasigualazero.png)

- Será validado que não é possível cadastrar vendas com uma string no campo quantidade

  - Se a venda tiver uma quantidade com valor, o resultado retornado deverá ser conforme exibido abaixo, com status http `422`:

![Vendas com string](./public/comprascomstring.png)

- Será validado que é possível criar uma venda com sucesso

  - Se a venda foi feita com sucesso, o resultado retornado deverá ser conforme exibido abaixo, com status http `200`:

![Cadastro de venda com sucesso](./public/cadastrodevendacomsucesso.png)

- Será validado que é possível criar várias vendas com sucesso

  - Se as vendas foi feita com sucesso, o resultado retornado deverá ser conforme exibido abaixo, com status http `200`:

![Cadastrar varias compras](./public/variascompras.png)

### 6 - Crie um endpoint para listar as vendas

- O endpoint deve ser acessível através do caminho (`/sales`) ou (`/sales/:id`);

- Através do caminho `/sales`, todas as vendas devem ser retornadas;

- Através do caminho `/sales/:id`, apenas a venda com o `id` presente na URL deve ser retornada;

**O que será verificado:**

- Será validado que todas as vendas estão sendo retornadas

  - Se todas vendas estão sendo listadas, o resultado retornado deverá ser conforme exibido abaixo, com status http `200`:

![Listar todas as vendas](./public/todasvendas.png)

- Será validado que é possível listar uma determinada venda

 - Se a venda esta sendo listada, o resultado retornado deverá ser conforme exibido abaixo, com status http `200`:

![Listar uma venda](./public/listaumavenda.png)

- Será validado que não é possível listar uma venda inexistente

  - Se a venda não esta sendo listada, o resultado retornado deverá ser conforme exibido abaixo, com status http `404`:

![Listar uma venda que não existe](./public/vendanaoexiste.png)

### 7 - Crie um endpoint para atualizar uma venda

- O endpoint deve ser acessível através do caminho (`/sales/:id`);

- O corpo da requisição deve receber a seguinte estrutura:

```json
[
  {
    "productId": "5f3ff849d94d4a17da707008",
    "quantity": 3
  }
]
```

- `quantity` deve ser um número inteiro maior que 0;

- Apenas a venda com o `id` presente na URL deve ser atualizada;

**O que será verificado:**

- Será validado que não é possível atualizar vendas com quantidade menor que zero

  - Se a venda tiver uma quantidade menor que zero, o resultado retornado deverá ser conforme exibido abaixo, com status http `422`:

![Atualizar venda menor que zero](./public/atualizarvendamenorquezero.png)

- Será validado que não é possível atualizar vendas com quantidade igual a zero

  - Se a venda tiver uma quantidade igual a zero, o resultado retornado deverá ser conforme exibido abaixo, com status http `422`:

![Atualizar venda igual zero](./public/atualizarvendaigualzero.png)

- Será validado que não é possível atualizar vendas com uma string no campo quantidade

  - Se a venda tiver uma quantidade do tipo string, o resultado retornado deverá ser conforme exibido abaixo, com status http `422`:

![Atualizar venda com string](./public/atualizarvendacomstring.png)

- Será validado que é possível atualizar uma vendas com sucesso

  - Se a venda for atualizada com sucesso, o resultado retornado deverá ser conforme exibido abaixo, com status http `200`:

![Atualizar uma venda com sucesso](./public/atualizarvendacomsucesso.png)

### 8 - Crie um endpoint para deletar uma venda

- O endpoint deve ser acessível através do caminho (`/sales/:id`);

- Apenas a venda com o `id` presente na URL deve ser deletado;

**O que será verificado:**

- Será validado que é possível deletar uma venda com sucesso

  - Se a venda foi deletada sucesso, o resultado retornado deverá ser conforme exibido abaixo, com status http `200` e será verificado depois que a venda não existe, com um GET nesse `id`, e este deverá retornar status http `404`, como é validado no requisito 6:

![Deletar uma venda com sucesso](./public/deletarumavendacomsucesso.png)

- Será validado que não é possível deletar uma venda que não existe

  - Se a venda não foi deletada sucesso, o resultado retornado deverá ser conforme exibido abaixo, com status http `422`:

![Deletar uma venda que não existe](./public/deletarumavendaquenaoexiste.png)

### 9 - Atualize a quantidade de produtos

- Ao realizar uma venda, atualizá-la ou deletá-la, você deve também atualizar a quantidade do produto em questão presente na `collection` responsável pelos produtos;

- Por exemplo: suponha que haja um produto chamado _Bola de Futebol_ e a sua propriedade `quantity` tenha o valor _10_. Caso seja feita uma venda com _8_ unidades desse produto, a quantidade do produto deve ser atualizada para _2_ , pois 10 - 8 = 2;

**O que será verificado:**

- Será validado que é possível a quantidade do produto atualize ao fazer uma compra

  - Ao fazer uma determinada venda, a quantidade do produto deverá ser atualizada.

- Será validado que é possível a quantidade do produto atualize ao deletar uma compra

  - Ao fazer deletar uma determinada venda, a quantidade do produto deverá ser atualizada para a quantidade que tinha antes de ter feito essa venda.

### 10 - Valide a quantidade de produtos

- Um produto nunca deve ter a quantidade em estoque menor que 0;

- Quando uma venda for realizada, garanta que a quantidade sendo vendida está disponível no estoque

**O que será verificado:**

- Será validado que o estoque do produto nunca fique com a quantidade menor que zero

  - Um produto não poderá ficar com a quantidade menor que zero, o resultado retornado deverá ser conforme exibido abaixo, com status http `404`:

![Compra maior que a quantidade](./public/compramaiorqueaquantidade.png)

## Bônus

## 11 - Escreva testes para seus models

- Utilize o mocha, chai e sinon para escrever seus testes

- Coloque todos os testes de models no arquivo `test/unit/models.js`

- Será validado que cobertura total das linhas dos arquivos na pasta `models` é maior ou igual a 80%

## 12 - Escreva testes para seus services

- Utilize o mocha, chai e sinon para escrever seus testes

- Coloque todos os testes de services no arquivo `test/unit/services.js`

- Será validado que cobertura total das linhas dos arquivos na pasta `services` é maior ou igual a 80%

## 13 - Escreva testes para seus controllers

- Utilize o mocha, chai e sinon para escrever seus testes

- Coloque todos os testes de controllers no arquivo `test/unit/controllers.js`

- Será validado que cobertura total das linhas dos arquivos na pasta `controllers` é maior ou igual a 80%

---
