# Documentação da API

## Introdução

Bem-vindo à documentação da API! Esta API foi desenvolvida para fornecer funcionalidades relacionadas à autenticação, sessões, carrinhos de compras e consulta de produtos. Ela se comunica com um banco de dados PostgreSQL para realizar operações de CRUD.
Este documento fornece uma documentação para o código Node.js que se conecta a um banco de dados PostgreSQL e oferece uma série de funções para acessar e manipular dados no banco de dados. O código é dividido em várias funções que realizam diferentes tarefas relacionadas ao gerenciamento de sessões, carrinhos de compras, pastéis e outros dados.

**Base URL:** `http://localhost:5550`

### Requisitos

Antes de usar este código, é importante garantir que você tenha as seguintes dependências instaladas:

1. Node.js: Certifique-se de que o Node.js esteja instalado na sua máquina.

2. Bibliotecas: Instale as dependências necessárias usando o gerenciador de pacotes npm (Node Package Manager). Você pode fazer isso executando o seguinte comando na pasta do projeto:

   ```bash
   npm install pg express
   ```

### Configuração do Banco de Dados

Antes de usar o código, você deve configurar as informações do banco de dados. As configurações do banco de dados são definidas no objeto `config`. Certifique-se de atualizar as seguintes propriedades:

- `user`: Nome de usuário do banco de dados.
- `host`: Host ou endereço IP do servidor PostgreSQL.
- `database`: Nome do banco de dados.
- `password`: Senha do banco de dados.
- `port`: Porta em que o PostgreSQL está sendo executado.
- `ssl`: Define se a conexão deve usar SSL (true/false).

## Funções Principais

A seguir, são documentadas as funções principais definidas no código:

#### `getId(email, type)`

- Descrição: Esta função recupera o ID de um usuário (adm ou cliente) com base no endereço de e-mail fornecido e no tipo de usuário.
- Parâmetros:
  - `email` (String): Endereço de e-mail do usuário.
  - `type` (String): Tipo de usuário ('adm' ou 'cliente').
- Retorno:
  - Retorna o ID do usuário se encontrado, caso contrário, retorna `null`.

#### `sessionIsOpen(email)`

- Descrição: Verifica se existe uma sessão aberta para um usuário (adm) com base no endereço de e-mail fornecido.
- Parâmetros:
  - `email` (String): Endereço de e-mail do usuário.
- Retorno:
  - Retorna `true` se houver uma sessão aberta, caso contrário, retorna `false`.

#### `auth(email)`

- Descrição: Verifica se um endereço de e-mail existe no banco de dados e retorna o tipo de usuário (adm ou cliente).
- Parâmetros:
  - `email` (String): Endereço de e-mail a ser verificado.
- Retorno:
  - Retorna o tipo de usuário ('adm', 'cliente') se o e-mail existir, caso contrário, retorna `false`.

#### `closeSession(email)`

- Descrição: Fecha uma sessão para um usuário (adm) com base no endereço de e-mail fornecido.
- Parâmetros:
  - `email` (String): Endereço de e-mail do usuário.
- Retorno:
  - Retorna `true` se a sessão foi fechada com sucesso, caso contrário, retorna `false`.

#### `openSession(email, h_termino)`

- Descrição: Abre uma nova sessão para um usuário (adm) com base no endereço de e-mail fornecido e no horário de término.
- Parâmetros:
  - `email` (String): Endereço de e-mail do usuário.
  - `h_termino` (String): Horário de término da sessão.
- Retorno:
  - Retorna `true` se a sessão foi aberta com sucesso, caso contrário, retorna `false`.

#### `showPasteis(consulta)`

- Descrição: Retorna uma lista de pasteis que correspondem a uma consulta específica no sabor ou na descrição do pastel.
- Parâmetros:
  - `consulta` (String): Consulta de pesquisa para os pasteis.
- Retorno:
  - Retorna um objeto contendo a quantidade de resultados e a lista de pasteis correspondentes.

#### `updateCarrinho(quantidade, id_carrinho, id_sessao, id_pastel)`

- Descrição: Atualiza a quantidade de pastéis em um carrinho de compras.
- Parâmetros:
  - `quantidade` (Number): Nova quantidade de pastéis.
  - `id_carrinho` (Number): ID do carrinho de compras.
  - `id_sessao` (Number): ID da sessão relacionada ao carrinho.
  - `id_pastel` (Number): ID do pastel a ser atualizado.
- Retorno:
  - Retorna `true` se a atualização foi bem-sucedida, caso contrário, retorna `false`.

#### `verifyFrete(email)`

- Descrição: Verifica se um cliente tem direito a frete grátis com base em determinados critérios.
- Parâmetros:
  - `email` (String): Endereço de e-mail do cliente.
- Retorno:
  - Retorna um objeto contendo informações sobre a verificação.

#### `detalhamentoCarrinho(email)`

- Descrição: Retorna detalhes dos itens em um carrinho de compras para um cliente específico.
- Parâmetros:
  - `email` (String): Endereço de e-mail do cliente.
- Retorno:
  - Retorna um objeto com detalhes do carrinho, incluindo sabor do pastel, quantidade e preço total.

#### `totalCarrinho(email)`

- Descrição: Retorna o valor total e a quantidade de pasteis em um carrinho de compras para um cliente específico.
- Parâmetros:
  - `email` (String): Endereço de e-mail do cliente.
- Retorno:
  - Retorna um objeto com o valor total e a quantidade de pasteis no carrinho.

#### `comprovanteExiste(id_carrinho)`

- Descrição: Verifica se existe um comprovante em um carrinho de compras com base no ID do carrinho.
- Parâmetros:
  - `id_carrinho` (Number): ID do carrinho de compras.
- Retorno:
  - Retorna informações sobre a existência de um comprovante.

#### `pasteisSessao(email)`

- Descrição: Retorna informações sobre os pasteis pedidos em uma sessão para um usuário (adm) com base no endereço de e-mail do adm.
- Parâmetros:
  - `email` (String): Endereço de e-mail do adm.
- Retorno:
  - Retorna informações sobre os pasteis pedidos na sessão, incluindo sabor, quantidade de pedidos e valor total.

#### `carrinhoSessao(id_sessao)`

- Descrição: Retorna informações sobre os carrinhos de compras em uma sessão com base no ID da sessão.
- Parâ

metros:
  - `id_sessao` (Number): ID da sessão.
- Retorno:
  - Retorna informações sobre os carrinhos de compras na sessão, incluindo nome do cliente, quantidade de pastéis, valor total e a existência de um comprovante.

#### `clienteAtivo(email)`

- Descrição: Verifica se um cliente está ativo em uma sessão com base no endereço de e-mail do cliente.
- Parâmetros:
  - `email` (String): Endereço de e-mail do cliente.
- Retorno:
  - Retorna informações sobre a ativação do cliente em uma sessão.

#### `sessionIsOpenNow()`

- Descrição: Retorna informações sobre as sessões atualmente abertas, incluindo o nome do adm e os horários de início e término.
- Retorno:
  - Retorna informações sobre as sessões abertas no momento.

### Exportação de Funções

No final do código, todas as funções mencionadas acima são exportadas em um objeto para que possam ser utilizadas em outros módulos ou aplicativos Node.js.

Certifique-se de entender o funcionamento de cada função antes de usá-las em seu projeto, e adapte-as conforme necessário para atender aos requisitos específicos do seu aplicativo.

## Endpoints

A API possui os seguintes endpoints:

### 1. Autenticação

#### 1.1 Autenticação de Login

- **URL:** `/auth`
- **Método:** GET
- **Parâmetros de consulta:**
  - `email` (string, obrigatório) - O email para autenticação.
- **Resposta de Sucesso:** Status 302
- **Exemplo de Uso:**
  ```
  GET /auth?email=usuario@exemplo.com
  ```

### 2. Sessões

#### 2.1 Abrir uma Sessão

- **URL:** `/open`
- **Método:** POST
- **Corpo da Solicitação (JSON):**
  - `email` (string, obrigatório) - O email do administrador.
  - `h_termino` (string, obrigatório) - Hora de término da sessão.
- **Resposta de Sucesso:** Status 201
- **Exemplo de Uso:**
  ```
  POST /open
  {
    "email": "admin@exemplo.com",
    "h_termino": "2023-09-27 18:00:00"
  }
  ```

#### 2.2 Fechar uma Sessão

- **URL:** `/close`
- **Método:** POST
- **Corpo da Solicitação (JSON):**
  - `email` (string, obrigatório) - O email do administrador.
- **Resposta de Sucesso:** Status 204 (sem conteúdo)
- **Exemplo de Uso:**
  ```
  POST /close
  {
    "email": "admin@exemplo.com"
  }
  ```

#### 2.3 Verificar Sessão Ativa

- **URL:** `/sessionopen`
- **Método:** GET
- **Resposta de Sucesso:** Status 200
- **Exemplo de Uso:**
  ```
  GET /sessionopen
  ```

### 3. Produtos

#### 3.1 Consultar Produtos

- **URL:** `/pasteis`
- **Método:** GET
- **Parâmetros de consulta:**
  - `q` (string, opcional) - Consulta por sabor ou descrição.
- **Resposta de Sucesso:** Status 200
- **Exemplo de Uso:**
  ```
  GET /pasteis?q=pastel de queijo
  ```

### 4. Carrinho de Compras

#### 4.1 Atualizar Carrinho

- **URL:** `/update`
- **Método:** POST
- **Corpo da Solicitação (JSON):**
  - `quantidade` (int, obrigatório) - A quantidade a ser atualizada.
  - `id_carrinho` (int, obrigatório) - O ID do carrinho.
  - `id_sessao` (int, obrigatório) - O ID da sessão.
  - `id_pastel` (int, obrigatório) - O ID do pastel.
- **Resposta de Sucesso:** Status 204 (sem conteúdo)
- **Exemplo de Uso:**
  ```
  POST /update
  {
    "quantidade": 3,
    "id_carrinho": 1,
    "id_sessao": 2,
    "id_pastel": 5
  }
  ```

#### 4.2 Detalhamento do Carrinho

- **URL:** `/detalhamento`
- **Método:** POST
- **Corpo da Solicitação (JSON):**
  - `email` (string, obrigatório) - O email do administrador.
- **Resposta de Sucesso:** Status 200
- **Exemplo de Uso:**
  ```
  POST /detalhamento
  {
    "email": "admin@exemplo.com"
  }
  ```

#### 4.3 Total do Carrinho

- **URL:** `/total`
- **Método:** POST
- **Corpo da Solicitação (JSON):**
  - `email` (string, obrigatório) - O email do administrador.
- **Resposta de Sucesso:** Status 200
- **Exemplo de Uso:**
  ```
  POST /total
  {
    "email": "admin@exemplo.com"
  }
  ```

#### 4.4 Verificar Comprovante

- **URL:** `/comprovante`
- **Método:** POST
- **Corpo da Solicitação (JSON):**
  - `id_carrinho` (int, obrigatório) - O ID do carrinho.
- **Resposta de Sucesso:** Status 200
- **Exemplo de Uso:**
  ```
  POST /comprovante
  {
    "id_carrinho": 1
  }
  ```

### 5. Relatórios

#### 5.1 Pasteis por Sessão

- **URL:** `/pasteisSessao`
- **Método:** POST
- **Corpo da Solicitação (JSON):**
  - `email` (string, obrigatório) - O email do administrador.
- **Resposta de Sucesso:** Status 200
- **Exemplo de Uso:**
  ```
  POST /pasteisSessao
  {
    "email": "admin@exemplo.com"
  }
  ```

#### 5.2 Carrinhos por Sessão

- **URL:** `/carrinhoSessao`
- **Método:** POST
- **Corpo da Solicitação (JSON):**
  - `id_sessao` (int, obrigatório) - O ID da sessão.
- **Resposta de Sucesso:** Status 200
- **Exemplo de Uso:**
  ```
  POST /carrinhoSessao
  {
    "id_sessao": 2
  }
  ```

#### 5.3 Cliente Ativo

- **URL:** `/clienteAtivo`
- **Método:** POST
- **Corpo da Solicitação (JSON):**
  - `email` (string, obrigatório) - O email do cliente.
- **Resposta de Sucesso:** Status 200
- **Exemplo de Uso:**
  ```
  POST

 /clienteAtivo
  {
    "email": "cliente@exemplo.com"
  }
  ```

## Respostas de Erro Comuns

- **Erro de Autenticação:** Status 404
- **Erro de Validação de Dados:** Status 400

Lembre-se de substituir as URLs e os exemplos de uso com os valores reais ao usar a API em um ambiente de produção. Certifique-se de que as solicitações incluam cabeçalhos apropriados, como tokens de autenticação, se necessário, e que as respostas sejam tratadas de acordo com os códigos de status retornados.
