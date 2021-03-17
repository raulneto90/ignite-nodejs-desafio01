# Ignite - NodeJS - Desafio 01

## :information_source: Informações do projeto

Uma aplicação de gerenciamento de Tarefas (em inglês Todos).
Nesta aplicação você pode se cadastrar como um usuário e registrar todas as tarefas que necessita fazer no seu dia a dia.

### Requisitos

- [X] O usuário deve poder se registrar na plataforma utilizando nome e login (username).
- [X] O usuário deve poder cadastrar uma tarefa (Todo).
- [X] O usuário deve poder editar uma tarefa (Todo).
- [X] O usuário deve poder visualizar todas as tarefas (Todo).
- [X] O usuário deve poder deletar uma tarefa (Todo).
- [X] O usuário deve poder marcar uma tarefa (Todo) como concluída.

### Regras de negócio

- [X] O usuário não deve poder se registrar na plataforma utilizando um login (username) já existente.
- [X] O usuário não deve poder cadastrar uma tarefa (Todo) se não passar o login de acesso.
- [X] O usuário não deve poder editar uma tarefa (Todo) se não passar o login de acesso.
- [X] O usuário não deve poder deletar uma tarefa (Todo) se não passar o login de acesso.
- [X] O usuário não deve poder marcar uma tarefa (Todo) como concluída se não passar o login de acesso.

## Específicação dos testes

Em cada teste, tem uma breve descrição no que sua aplicação deve cumprir para que o teste passe.

Caso você tenha dúvidas quanto ao que são os testes, e como interpretá-los, dê uma olhada em **[nosso FAQ](https://www.notion.so/FAQ-Desafios-ddd8fcdf2339436a816a0d9e45767664)**

Para esse desafio, temos os seguintes testes:

### Testes de usuários

- **Should be able to create a new user**

Para que esse teste passe, você deve permitir que um usuário seja criado e retorne um json com o usuário criado. Você pode ver o formato de um usuário [aqui](https://www.notion.so/Desafio-01-Conceitos-do-Node-js-59ccb235aecd43a6a06bf09a24e7ede8). 

Também é necessário que você retorne a resposta com o código `201`.

- **Should not be able to create a new user when username already exists**

Para que esse teste passe, antes de criar um usuário você deve validar se outro usuário com o mesmo `username` já existe. Caso exista, retorne uma resposta com status `400` e um json no seguinte formato:

```jsx
{
	error: 'Mensagem do erro'
}
```

A mensagem pode ser de sua escolha, desde que a propriedade seja `error`.

### Testes de *todos*

**Middleware**

Para completar todos os testes referentes à *todos* é necessário antes ter completado o código que falta no middleware `checkExistsUserAccount`. Para isso, você deve pegar o `username` do usuário no header da requisição, verificar se esse usuário existe e então colocar esse usuário dentro da `request` antes de chamar a função `next`. Caso o usuário não seja encontrado, você deve retornar uma resposta contendo status `404` e um json no seguinte formato:

```jsx
{
	error: 'Mensagem do erro'
}
```

**Observação:** O username deve ser enviado pelo header em uma propriedade chamada `username`:

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5c538c34-498a-4789-9bb4-0f286d9b2cf2/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5c538c34-498a-4789-9bb4-0f286d9b2cf2/Untitled.png)

- **Should be able to list all user's todos**

Para que esse teste passe, na rota GET `/todos` é necessário pegar o usuário que foi repassado para o `request` no middleware `checkExistsUserAccount` e então retornar a lista `todos` que está no objeto do usuário conforme foi criado para satisfazer o [primeiro teste](https://www.notion.so/Desafio-01-Conceitos-do-Node-js-59ccb235aecd43a6a06bf09a24e7ede8).

- **Should be able to create a new todo**

Para que esse teste passe, na rota POST `/todos` é necessário pegar o usuário que foi repassado para o `request` no middleware `checkExistsUserAccount`, pegar também o `title` e o `deadline` do corpo da requisição e adicionar um novo *todo* na lista `todos` que está no objeto do usuário.

Lembre-se de seguir a estrutura padrão de um *todo* como mostrado [aqui](https://www.notion.so/Desafio-01-Conceitos-do-Node-js-59ccb235aecd43a6a06bf09a24e7ede8). 

- **Should be able to update a todo**

Para que esse teste passe, na rota PUT `/todos/:id` é necessário atualizar um *todo* existente, recebendo o `title` e o `deadline` pelo corpo da requisição e o `id` presente nos parâmetros da rota.

- **Should not be able to update a non existing todo**

Para que esse teste passe, você não deve permitir a atualização de um *todo* que não existe e retornar uma resposta contendo um status `404` e um json no seguinte formato: 

```jsx
{
	error: 'Mensagem do erro'
}
```

- **Should be able to mark a todo as done**

Para que esse teste passe, na rota PATCH `/todos/:id/done` você deve mudar a propriedade `done`de um *todo* de `false` para `true`, recebendo o `id` presente nos parâmetros da rota.

- **Should not be able to mark a non existing todo as done**

Para que esse teste passe, você não deve permitir a mudança da propriedade `done` de um *todo* que não existe e retornar uma resposta contendo um status `404` e um json no seguinte formato: 

```jsx
{
	error: 'Mensagem do erro'
}
```

- **Should be able to delete a todo**

Para que esse teste passe, DELETE `/todos/:id` você deve permitir que um *todo* seja excluído usando o `id` passado na rota. O retorno deve ser apenas um status `204` que representa uma resposta sem conteúdo.

- **Should not be able to delete a non existing todo**

Para que esse teste passe, você não deve permitir excluir um *todo* que não exista e retornar uma resposta contendo um status `404` e um json no seguinte formato:

```jsx
{
	error: 'Mensagem do erro'
}
```

## :floppy_disk: Como utilizar este projeto

Para baixar este projeto é necessário que esteja instalado em seu computador o NodeJS e o Yarn.
No terminal:

```bash
$ git clone https://github.com/raulneto90/ignite-nodejs-desafio01

# Acesse o diretório do projeto
$ cd ignite-nodejs-desafio01

# Instalar as dependências
$ yarn

# Executar o projeto em desenvolvimento
$ yarn dev
```
---
Feito com ❤ por Raul Neto. Me siga no [Linkedin](https://www.linkedin.com/in/raul-neto-777bb988/)
