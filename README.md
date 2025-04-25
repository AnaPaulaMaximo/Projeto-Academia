
# API de Gerenciamento de Clientes

Este é um serviço de API RESTful desenvolvido com Flask, integrado ao Firebase Firestore para o gerenciamento de clientes. A API oferece operações de CRUD (Create, Read, Update, Delete) para clientes, incluindo a busca de clientes com base em campos específicos e a listagem de todos os clientes cadastrados.

## Link do vercel
[Clique aqui](https://projeto-academia-nu.vercel.app/)


## Funcionalidades

A API possui as seguintes funcionalidades:

- **Cadastrar Cliente** (`POST /clientes`)
- **Buscar Cliente por Campo Específico** (`GET /clientes/<campo>/<busca>`)
- **Alterar Cadastro de Cliente** (`PUT /clientes/<id>`)
- **Excluir Cadastro de Cliente** (`DELETE /clientes/<id>`)
- **Listar Todos os Clientes** (`GET /clientes/lista`)
- **Testar a Conectividade da API** (`GET /`)

## Requisitos

- Python 3.x
- Flask
- Firebase Admin SDK
- Flask-CORS
- python-dotenv

## Configuração Inicial

1. Clone o repositório para sua máquina local.
2. Instale as dependências:
   ```bash
   pip install -r requirements.txt
   ```
3. Configure a chave de autenticação do Firebase:
   - Crie um projeto no Firebase.
   - Gere uma chave de serviço (arquivo JSON) do Firebase Admin SDK.
   - Coloque o conteúdo dessa chave no arquivo `.env` como `CONFIG_FIREBASE`.
   - Exemplo de arquivo `.env`:
     ```
     CONFIG_FIREBASE='{"type": "service_account", "project_id": "seu-projeto-id", ...}'
     ```
4. Inicie o servidor Flask:
   ```bash
   python app.py
   ```

## Endpoints

### `GET /`
- **Descrição**: Teste básico da conectividade da API.
- **Resposta**: `API ON`

### `GET /clientes/<campo>/<busca>`
- **Descrição**: Busca clientes com base no campo fornecido.
- **Parâmetros**:
  - `campo`: Pode ser `id`, `nome`, `cpf`, `status` ou `plano`.
  - `busca`: O valor a ser pesquisado.
- **Resposta**: 
  - `200 OK`: Lista de clientes encontrados.
  - `404 Not Found`: Se nenhum cliente for encontrado.

### `POST /clientes`
- **Descrição**: Cadastrar um novo cliente.
- **Corpo da Requisição** (JSON):
  ```json
  {
    "nome": "Nome do Cliente",
    "cpf": "12345678901",
    "status": "true",
    "foto_url": "http://exemplo.com/foto.jpg",
    "plano": "mensal"
  }
  ```
- **Resposta**:
  - `201 Created`: Cliente cadastrado com sucesso.
  - `400 Bad Request`: Se algum campo obrigatório estiver ausente ou inválido.

### `PUT /clientes/<id>`
- **Descrição**: Atualiza os dados de um cliente existente.
- **Parâmetros**:
  - `id`: ID do cliente a ser atualizado.
- **Corpo da Requisição** (JSON):
  ```json
  {
    "nome": "Novo Nome",
    "cpf": "98765432100",
    "status": "false",
    "foto_url": "http://exemplo.com/nova-foto.jpg",
    "plano": "anual"
  }
  ```
- **Resposta**:
  - `200 OK`: Cadastro atualizado com sucesso.
  - `404 Not Found`: Se o cliente não for encontrado.

### `DELETE /clientes/<id>`
- **Descrição**: Excluir um cliente pelo seu ID.
- **Parâmetros**:
  - `id`: ID do cliente a ser excluído.
- **Resposta**:
  - `200 OK`: Cliente excluído com sucesso.
  - `404 Not Found`: Se o cliente não for encontrado.

### `GET /clientes/lista`
- **Descrição**: Lista todos os clientes cadastrados.
- **Resposta**:
  - `200 OK`: Lista de todos os clientes.
  - `404 Not Found`: Se nenhum cliente for encontrado.

## Estrutura do Banco de Dados

A API utiliza o Firebase Firestore para armazenar as informações dos clientes. A estrutura básica para cada cliente é:

```json
{
  "id": "ID do Cliente",
  "nome": "Nome do Cliente",
  "cpf": "CPF do Cliente",
  "status": "Status do Cliente (true ou false)",
  "foto_url": "URL da foto do Cliente",
  "plano": "Plano do Cliente (mensal, trimestral, semestral, anual)"
}
```

### Tabela `clientes`
Armazena os dados de todos os clientes, com campos como `nome`, `cpf`, `status`, `foto_url` e `plano`.

### Tabela `controle_id`
Responsável por gerenciar o contador de IDs para a criação de novos clientes.

## Exemplos de Requisição

### Criar Cliente
```bash
POST /clientes
```
Body:
```json
{
  "nome": "João Silva",
  "cpf": "12345678901",
  "status": "true",
  "foto_url": "http://example.com/photo.jpg",
  "plano": "mensal"
}
```

### Buscar Cliente por Nome
```bash
GET /clientes/nome/João Silva
```

### Atualizar Cliente
```bash
PUT /clientes/1
```
Body:
```json
{
  "nome": "João Silva Atualizado",
  "cpf": "12345678901",
  "status": "false",
  "foto_url": "http://example.com/newphoto.jpg",
  "plano": "anual"
}
```

### Excluir Cliente
```bash
DELETE /clientes/1
```

## Erros Comuns

- **400 Bad Request**: Se algum campo obrigatório estiver ausente ou inválido.
- **404 Not Found**: Se o cliente não for encontrado em operações de busca ou atualização.

## Conclusão

Essa API oferece uma maneira simples e eficiente de gerenciar clientes, com integração ao Firebase Firestore. Pode ser expandida conforme as necessidades do projeto, oferecendo novas funcionalidades ou aprimorando as existentes.
