### Login

POST /login <br/>
POST /signin

Qualquer um desses 2 endpoints pode ser usado para realizar login com um dos usuários cadastrados na lista de "Users"

<h2 align ='start'> API </h2>

https://api-time-stamp.herokuapp.com

<h2 align ='center'> Login usuário </h2>

`POST /login`

```json
{
  "email": "user@mail.com",
  "password": "senha123"
}
```

Caso dê tudo certo, a resposta será assim:

`FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Imluc3RydXRvckBtYWlsLmNvbSIsImlhdCI6MTY2MTk0ODEzMiwiZXhwIjoxNjYxOTUxNzMyLCJzdWIiOiIzIn0.7zzLwKWHqtefUneP5JhyIp-iVFVFwtIw8_L5C21sw8U",
  "user": {
    "email": "instrutor@mail.com",
    "name": "Naruto",
    "age": 38,
    "id": 3
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

<h2 align ='center'> Mostrar vídeos </h2>

`GET /videos`

Retorna todos os videos criados, por todos os usuarios

```json
[
  {
    "url": "https://demos-kenzie-academy-brasil.s3.amazonaws.com/mar22/m3/Sprint_1/GMT20220719-123327_Recording_1760x900.mp4",
    "userId": 1,
    "marks ": [
      {
        "time_video": "02:30",
        "title": "react-js222"
      },
      {
        "time_video": "04:30",
        "title": "json-server"
      }
    ],
    "id": 1
  },
  {
    "url": "https://demos-kenzie-academy-brasil.s3.amazonaws.com/mar22/m3/Sprint_1/GMT20220719-123327_Recording_1760x900.mp4",
    "sprint": 1,
    "userId": 2,
    "day": "friday",
    "isExtra": false,
    "marks ": [],
    "id": 3
  },
  {
    "url": "https://demos-kenzie-academy-brasil.s3.amazonaws.com/mar22/m3/Sprint_1/GMT20220719-123327_Recording_1760x900.mp4",
    "userId": 3,
    "marks ": [
      {
        "time_video": "04:25",
        "title": "react-js222"
      },
      {
        "time_video": "10:15",
        "title": "json-server"
      }
    ],
    "id": 8
  }
]
```

`GET /videos?userId=:userId`

Retorna todos os videos criados pelo usuario sem necessidade de autorização

```json
[
  {
    "url": "https://demos-kenzie-academy-brasil.s3.amazonaws.com/mar22/m3/Sprint_1/GMT20220719-123327_Recording_1760x900.mp4",
    "userId": 3,
    "marks ": [
      {
        "time_video": "04:25",
        "title": "react-js222"
      },
      {
        "time_video": "10:15",
        "title": "json-server"
      }
    ],
    "id": 5
  },
  {
    "url": "https://demos-kenzie-academy-brasil.s3.amazonaws.com/mar22/m3/Sprint_1/GMT20220719-123327_Recording_1760x900.mp4",
    "userId": 3,
    "marks ": [
      {
        "time_video": "04:25",
        "title": "react-js222"
      },
      {
        "time_video": "10:15",
        "title": "json-server"
      }
    ],
    "id": 6
  }
]
```

## Rotas que necessitam de autorização

A partir daqui, todas as rotas necessitam de autenticação

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

> Authorization: Bearer {token}

<h2 align ='center'> Acessar usuário </h2>

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
  "module": "3",
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

`POST /videos`

```json
{
  "url": "https://demos-kenzie-academy-brasil.s3.amazonaws.com/mar22/m3/Sprint_1/GMT20220719-123327_Recording_1760x900.mp4",
  "userId": 3,
  "marks ": [
    {
      "time_video": "04:25",
      "title": "react-js222"
    },
    {
      "time_video": "10:15",
      "title": "json-server"
    }
  ]
}
```

`FORMATO DA RESPOSTA - STATUS 201`

```json
{
  "url": "https://demos-kenzie-academy-brasil.s3.amazonaws.com/mar22/m3/Sprint_1/GMT20220719-123327_Recording_1760x900.mp4",
  "userId": 3,
  "marks ": [
    {
      "time_video": "04:25",
      "title": "react-js222"
    },
    {
      "time_video": "10:15",
      "title": "json-server"
    }
  ],
  "id": 5
}
```

`GET /users/:id/videos`

Caso dê tudo certo, irá retornar

`FORMATO DA RESPOSTA - STATUS 200`

```json
[
  {
    "url": "https://demos-kenzie-academy-brasil.s3.amazonaws.com/mar22/m3/Sprint_1/GMT20220719-123327_Recording_1760x900.mp4",
    "userId": 2,
    "marks ": [
      {
        "time_video": "04:25",
        "title": "react-js222"
      },
      {
        "time_video": "10:15",
        "title": "json-server"
      }
    ],
    "id": 4
  }
    {
    "url": "https://demos-kenzie-academy-brasil.s3.amazonaws.com/mar22/m3/Sprint_1/GMT20220719-123327_Recording_1760x900.mp4",
    "userId": 2,
    "marks ": [
      {
        "time_video": "14:25",
        "title": "react-js252"
      },
      {
        "time_video": "19:15",
        "title": "json-auth"
      }
    ],
    "id": 5
  }
]
```

`PATCH /videos/:idVideo`

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

```json
{}
```

Caso dê tudo certo, irá retornar

`FORMATO DA RESPOSTA - STATUS 200`

```json
{}
```
