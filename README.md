# projeto-todo-list

## Descrição

Este projeto é um MVP (Produto Viável Mínimo) de um aplicativo de gerenciamento de tarefas inspirado no Trello. A ideia é criar uma interface simples e intuitiva onde o usuário pode organizar suas tarefas em três colunas: "To Do", "Doing" e "Done".

## Funcionalidades

- Interface Drag-and-Drop: Os usuários poderão arrastar e soltar cartões entre as colunas para atualizar o status de suas tarefas.
- Colunas de Status: Cada tarefa pode estar em um dos três status: "To Do", "Doing" e "Done".

## Objetivo

O objetivo deste projeto é fornecer uma ferramenta básica para gerenciamento de tarefas, com foco na simplicidade e na usabilidade. Este MVP será a base para futuras iterações e adições de funcionalidades.

## Descrição Técnica

### Estrutura da Tabela de Cards

```bash
- id: (seria uma boa isso ser um UUID? uma chave primária, gerada automaticamente )
- titulo: string (obrigatório, limite de caracteres pode ser definido!)
- descricao: string (opcional)
- status: enum ('TO_DO', 'DOING', 'DONE') (obrigatório, padrão: 'TO_DO')
- created_at: datetime (obrigatório, gerado na criação)
- updated_at: datetime (atualizado automaticamente em qualquer modificação ou vale a pena criar um específico para quando é movido para doing?)
- finished_at: datetime (atualizado apenas quando o status muda para 'DONE')
```

### Endpoints da API

1. Criação de Card
   Método: POST
   Endpoint: `/cards`

Requisição:

```bash
{
  "titulo": "string",
  "descricao": "string"
}
```

Resposta:

```bash
{
  "id": "UUID",
  "titulo": "string",
  "descricao": "string",
  "status": "TO_DO",
  "created_at": "datetime",
  "updated_at": "datetime",
  "finished_at": null
}

```

2. Puxar Todos os Cards
   Método: GET
   Endpoint: `/cards`

Resposta:

```bash
[
  {
    "id": "UUID",
    "titulo": "string",
    "descricao": "string",
    "status": "TO_DO/DOING/DONE",
    "created_at": "datetime",
    "updated_at": "datetime",
    "finished_at": "datetime|null"
  },
  ...
]
```

3. Iniciar um Card (Mover para "DOING")
   Método: PUT
   Endpoint: `/cards/:id/start`

Resposta:

```bash
{
  "id": "UUID",
  "status": "DOING",
  "updated_at": "datetime"
}
```

4. Finalizar um Card (Mover para "DONE")
   Método: PUT
   Endpoint: `/cards/:id/finish`

Resposta:

```bash
{
  "id": "UUID",
  "status": "DONE",
  "updated_at": "datetime",
  "finished_at": "datetime"
}
```
