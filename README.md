# API de Gerenciamento de Usuários

API REST construída com Node.js puro para gerenciamento de usuários, utilizando apenas módulos nativos do Node.js sem frameworks externos.

## Descrição

Este projeto implementa uma API RESTful completa com operações CRUD (Create, Read, Update, Delete) para gerenciamento de usuários. O projeto também inclui exemplos práticos de trabalho com Streams do Node.js.

## Tecnologias

- Node.js
- HTTP nativo (node:http)
- File System (node:fs/promises)
- Streams (node:stream)
- JSON para persistência de dados

## Estrutura do Projeto

```
.
├── src/
│   ├── server.js                 # Servidor HTTP principal
│   ├── routes.js                 # Definição das rotas da API
│   ├── database.js               # Classe de gerenciamento do banco de dados
│   ├── middlewares/
│   │   └── json.js              # Middleware para parsing de JSON
│   └── utils/
│       ├── build-route-path.js  # Construtor de regex para rotas
│       └── extract-query-params.js # Extrator de query parameters
├── streams/
│   ├── fundamentals.js          # Exemplos básicos de streams
│   ├── fake-upload-to-http-stream.js # Exemplo de upload via stream
│   ├── stream-http-server.js    # Servidor HTTP com streams
│   └── buffer.js                # Exemplo de Buffer
├── db.json                      # Banco de dados JSON
└── package.json
```

## Funcionalidades

### Rotas da API

**GET /users**
- Lista todos os usuários
- Suporta busca via query parameter `?search=termo`
- Busca por nome ou email

**POST /users**
- Cria um novo usuário
- Corpo da requisição: `{ "name": "string", "email": "string" }`
- Retorna status 201

**PUT /users/:id**
- Atualiza um usuário existente
- Corpo da requisição: `{ "name": "string", "email": "string" }`
- Retorna status 204

**DELETE /users/:id**
- Remove um usuário
- Retorna status 204

### Banco de Dados

O projeto utiliza um sistema de banco de dados simples baseado em arquivo JSON (`db.json`). A classe `Database` implementa:

- **select**: Busca registros com filtros opcionais
- **insert**: Insere novos registros
- **update**: Atualiza registros existentes
- **delete**: Remove registros

Todas as operações são persistidas automaticamente no arquivo JSON.

### Exemplos de Streams

O projeto inclui exemplos práticos de trabalho com Streams:

- **Readable Streams**: Leitura de dados de forma assíncrona
- **Writable Streams**: Escrita de dados
- **Transform Streams**: Transformação de dados em tempo real
- Exemplos de piping entre streams

## Instalação

```bash
npm install
```

## Uso

### Iniciar o servidor

```bash
npm run dev
```

O servidor será iniciado na porta 3333.

### Exemplos de Requisições

**Listar usuários:**
```bash
curl http://localhost:3333/users
```

**Buscar usuários:**
```bash
curl http://localhost:3333/users?search=geninho
```

**Criar usuário:**
```bash
curl -X POST http://localhost:3333/users \
  -H "Content-Type: application/json" \
  -d '{"name":"João Silva","email":"joao@example.com"}'
```

**Atualizar usuário:**
```bash
curl -X PUT http://localhost:3333/users/ID_DO_USUARIO \
  -H "Content-Type: application/json" \
  -d '{"name":"João Santos","email":"joao.santos@example.com"}'
```

**Deletar usuário:**
```bash
curl -X DELETE http://localhost:3333/users/ID_DO_USUARIO
```

## Características Técnicas

### Roteamento Dinâmico

O sistema de rotas utiliza expressões regulares para matching de URLs e captura de parâmetros dinâmicos através de named groups.

### Middleware de JSON

Implementação customizada de middleware para parsing de corpo de requisições JSON utilizando Buffers e Streams.

### Persistência de Dados

Sistema de persistência automática que salva todas as alterações no banco de dados em arquivo JSON de forma assíncrona.

### Suporte a Query Parameters

Extração e parsing automático de query parameters das URLs para filtros e buscas.

## Scripts Disponíveis

- `npm run dev`: Inicia o servidor em modo watch (reinicia automaticamente ao detectar mudanças)

## Observações

- O banco de dados é criado automaticamente no primeiro uso
- Todos os IDs são gerados usando UUID v4
- As buscas não são case-sensitive
- O projeto utiliza ES Modules (type: "module")

## Licença

ISC