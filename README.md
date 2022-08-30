# json-server-base

Esse é o repositório com a base de JSON-Server + JSON-Server-Auth já configurada, feita para ser usada no desenvolvimento das API's nos Projetos Front-end.

## Endpoints

Assim como a documentação do JSON-Server-Auth traz (https://www.npmjs.com/package/json-server-auth), existem 3 endpoints que podem ser utilizados para cadastro e 2 endpoints que podem ser usados para login.

### Cadastro

POST /register <br/>
POST /signup <br/>
POST /users

Qualquer um desses 3 endpoints irá cadastrar o usuário na lista de "Users", sendo que os campos obrigatórios são os de email e password.
Você pode ficar a vontade para adicionar qualquer outra propriedade no corpo do cadastro dos usuários.

### Login

POST /login <br/>
POST /signin

Qualquer um desses 2 endpoints pode ser usado para realizar login com um dos usuários cadastrados na lista de "Users"

<h2 align ='center'> Login usuário </h2>

`POST /login`

```json
{
  "email": "user@email.com",
  "password": "senha123"
}
```

Caso dê tudo certo, a resposta será assim:

`FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InVzZXJAZW1haWwuY29tIiwiaWF0IjoxNjYxODc0MjI1LCJleHAiOjE2NjE4Nzc4MjUsInN1YiI6IjIifQ.2hITQNNZqC9WDTiR-QiaawfMteWAtshTdklwnifNfn8",
  "user": {
    "email": "user@email.com",
    "module": "M3",
    "id": 2
  }
}
```

<h2 align ='center'> Possíveis erros </h2>

Caso o e-mail esteja errado

` FORMATO DA RESPOSTA - STATUS 400`

```json
{
"Cannot find user"
}
```

Caso a senha esteja errado

` FORMATO DA RESPOSTA - STATUS 400`

```json
{
"Incorrect password"
}
```

<h2 align ='center'> Acessar usuário </h2>

## Rotas que necessitam de autorização

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

> Authorization: Bearer {token}

Após o usuário estar logado, ele deve conseguir postar videos e excluir videos. Assim como adicionar marcadores,
editar marcadores e deletar marcadores

`GET /users/:id -`

```json
{
 "Não há necessidade de passar nada como parametro"
}
```

`FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "email": "user@email.com",
  "password": "$2a$10$8DKEi3y79/MUeI20UD6EFuoRDCMYwFUmeg1OWwXIakydT9eTBVYf2",
  "module": "M3",
  "id": 2
}
```

<h2 align ='center'> Possíveis erros </h2>

Caso não tenha informado o token, irá retornar:

`FORMATO DA RESPOSTA - STATUS 401`

```json
{
"Missing token"
}
```

Caso não tenha sido informado o ID

`FORMATO DA RESPOSTA - STATUS 403`

```json
{"Private resource access: entity must have a reference to the owner id"}
```

<h2 align ='center'> Cadastrar vídeos </h2>

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

> Authorization: Bearer {token}

`POST /videos/`

```json
{
  "url": "https://demos-kenzie-academy-brasil.s3.amazonaws.com/mar22/m3/Sprint_1/GMT20220719-123327_Recording_1760x900.mp4",
  "bookmarks": "02:48, 15:25",
  "title": "Abordando sobre useEffect, Abordando sobre useState",
  "userId": 4
}
```

Caso dê tudo certo, irá retornar

`FORMATO DA RESPOSTA - STATUS 201`

```json
{
  "url": "https://demos-kenzie-academy-brasil.s3.amazonaws.com/mar22/m3/Sprint_1/GMT20220719-123327_Recording_1760x900.mp4",
  "bookmarks": "02:48, 15:25",
  "title": "Abordando sobre useEffect, Abordando sobre useState",
  "userId": 4,
  "id": 1
}
```

`POST /users/:id/videos`

> Authorization: Bearer {token}

Caso dê tudo certo, irá retornar

`FORMATO DA RESPOSTA - STATUS 200`

```json
[
  {
    "url": "https://demos-kenzie-academy-brasil.s3.amazonaws.com/mar22/m3/Sprint_1/GMT20220719-123327_Recording_1760x900.mp4",
    "bookmarks": "02:48, 15:25",
    "title": "Abordando sobre useEffect, Abordando sobre useState",
    "userId": 4,
    "id": 1
  }
]
```

`PATCH /videos/:idVideo`

> Authorization: Bearer {token}

```json
{
  "bookmarks": "03:48, 15:25"
}
```

Caso dê tudo certo, irá retornar

`FORMATO DA RESPOSTA - STATUS 200`

```json
[
  {
    "url": "https://demos-kenzie-academy-brasil.s3.amazonaws.com/mar22/m3/Sprint_1/GMT20220719-123327_Recording_1760x900.mp4",
    "bookmarks": "03:48, 15:25",
    "title": "Abordando sobre useEffect, Abordando sobre useState",
    "userId": 4,
    "id": 1
  }
]
```

`DELETE /videos/:idVideo`

> Authorization: Bearer {token}

```json
{}
```

Caso dê tudo certo, irá retornar

`FORMATO DA RESPOSTA - STATUS 200`

```json
{}
```
