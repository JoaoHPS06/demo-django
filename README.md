# 🐍 Demo Django — Parte 3: Modelos e Relacionamentos

> **Disciplina:** Programação Web  
> **Aluno:** [João Henrique Pedrosa de Souza]  
> **Branch:** [`bcc481-django-parte3`](https://github.com/SEU_USUARIO/demo-django/tree/bcc481-django-parte3)

---

## 📋 Descrição

Continuação do projeto `demo-django`, construída como parte do **Roteiro 3** da disciplina de Programação Web. A partir do projeto da Parte 2, esta etapa introduz relacionamentos entre modelos no Django ORM:

- Criação do modelo `Categoria` com relacionamento **um-para-muitos** com `Mensagem`
- Uso de `ForeignKey` com `on_delete=models.SET_NULL`
- Geração da migration que cria a nova tabela e a coluna de chave estrangeira
- Registro de `Categoria` no painel Admin com filtro lateral por categoria
- Exibição do "selo" de categoria no template com proteção via `{% if %}`
- Exploração do relacionamento inverso via `related_name` no shell do Django

---

## 📸 Sistema em execução

### Admin — listagem de mensagens com coluna Categoria e filtro lateral

> Após a migration, o painel exibe a coluna `Categoria` na listagem e um filtro lateral para filtrar mensagens por categoria.

<!-- Substitua pela sua captura de tela -->
![Admin mensagens com categoria](imagens/admin-mensagens-categoria.png)

### Admin — cadastro de Categorias

> Nova seção no painel admin para criar e gerenciar categorias (ex.: "Aviso", "Dúvida", "Sugestão").

<!-- Substitua pela sua captura de tela -->
![Admin cadastro de categorias](imagens/admin-categorias.png)

### Página principal com selos de categoria

> Cada mensagem exibe um "selo" colorido com o nome da categoria. Mensagens sem categoria não exibem o selo (proteção via `{% if m.categoria %}`).

<!-- Substitua pela sua captura de tela -->
![Página principal com selos](imagens/page-mensagens-com-categoria.png)

---

## 📚 Conceitos abordados neste roteiro

- Relacionamento **um-para-muitos** (1:N) com `ForeignKey`
- Parâmetros `on_delete`, `null`, `blank` e `related_name`
- Migrations incrementais para alterações de schema
- Inspeção do banco via `dbshell` e `.schema`
- `list_filter` no Django Admin para filtro lateral
- Acesso a campos de tabelas relacionadas no template com ponto (`m.categoria.nome`)
- Tag condicional `{% if %}` no Django Template Language
- Acesso inverso via `related_name` no ORM
- Shell interativo do Django (`manage.py shell`)
