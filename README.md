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
  "email": "m1@intrutor.com",
  "password": "intrutor@$123456"
}
```

Caso dê tudo certo, a resposta será assim:

`FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im0xQGludHJ1dG9yLmNvbSIsImlhdCI6MTY2MjQyNzgzOCwiZXhwIjoxNjYyNDMxNDM4LCJzdWIiOiIzIn0.yPOWfkHfR1qQl5R0gtUJGZCgj_R4vVgNmFhwieMACG0",
  "user": {
    "email": "m1@intrutor.com",
    "name": "Instrutor M1",
    "module": 1,
    "isAdmin": true,
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

`GET /videos?moduleId=3&&sprintId=2`

```json
[
  {
    "url": "https://demos-kenzie-academy-brasil.s3.amazonaws.com/mar22/m3/Sprint_1/GMT20220718-123537_Recording_1920x1080.mp4",
    "sprintId": 2,
    "day": "segunda",
    "extra": false,
    "moduleId": 3,
    "userId": 3,
    "created_at": "18/07/22",
    "updated_at": "05/09/22",
    "marks": [
      {
        "id": "1",
        "time_video": "02:30",
        "title": "react-js222"
      },
      {
        "id": 2,
        "time_video": "04:30",
        "title": "json-server"
      }
    ],
    "id": 1
  }
]
```

## Rotas que necessitam de autorização

A partir daqui, todas as rotas necessitam de autenticação

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

> Authorization: Bearer {token}

<h2 align ='center'> Cadastrar vídeos </h2>

`POST /videos`

```json
{
  "url": "https://demos-kenzie-academy-brasil.s3.amazonaws.com/mar22/m3/Sprint_1/GMT20220718-123537_Recording_1920x1080.mp4",
  "sprintId": 1,
  "day": "segunda",
  "extra": false,
  "moduleId": 3,
  "userId": 3,
  "created_at": "18/07/22",
  "updated_at": "05/09/22",
  "marks": [
    {
      "id": "1",
      "time_video": "02:30",
      "title": "react-js222"
    },
    {
      "id": 2,
      "time_video": "04:30",
      "title": "json-server"
    }
  ]
}
```

`FORMATO DA RESPOSTA - STATUS 201`

```json
{
  "url": "https://demos-kenzie-academy-brasil.s3.amazonaws.com/mar22/m3/Sprint_1/GMT20220718-123537_Recording_1920x1080.mp4",
  "sprintId": 1,
  "day": "segunda",
  "extra": false,
  "moduleId": 3,
  "userId": 3,
  "created_at": "18/07/22",
  "updated_at": "05/09/22",
  "marks": [
    {
      "id": "1",
      "time_video": "02:30",
      "title": "react-js222"
    },
    {
      "id": 2,
      "time_video": "04:30",
      "title": "json-server"
    }
  ],
  "id": 1
}
```

`PUT /videos/:id`

```json
{
   "marks": [
    {
      "id": "1",
      "time_video": "02:50",
      "title": "react-js232"
    },
    {
      "id": 2,
      "time_video": "05:10",
      "title": "json-server"
    }
}
```

Caso dê tudo certo, irá retornar

`FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "url": "https://demos-kenzie-academy-brasil.s3.amazonaws.com/mar22/m3/Sprint_1/GMT20220718-123537_Recording_1920x1080.mp4",
  "sprintId": 1,
  "day": "segunda",
  "extra": false,
  "moduleId": 3,
  "userId": 3,
  "created_at": "18/07/22",
  "updated_at": "06/09/22",
  "marks": [
    {
      "id": "1",
      "time_video": "02:50",
      "title": "react-js232"
    },
    {
      "id": 2,
      "time_video": "05:10",
      "title": "json-server"
    }
  ],
  "id": 1
}
```

`DELETE /videos/:id`

```json
{}
```

Caso dê tudo certo, irá retornar

`FORMATO DA RESPOSTA - STATUS 200`

```json
{}
```
