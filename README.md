# 🐍 Demo Django — Parte 1: Projeto Inicial

> **Disciplina:** Programação Web  
> **Aluno:** [João Henrique Pedrosa de Souza]  
> **Branch:** [`bcc481-django-parte1`](https://github.com/SEU_USUARIO/SEU_REPOSITORIO/tree/bcc481-django-parte1)

---

## 📋 Descrição

Projeto de demonstração construído como parte do **Roteiro 1** da disciplina de Programação Web. Implementa um site simples de uma página utilizando **Django 5.1**, estilizado com **Tailwind CSS via CDN**, persistindo dados em **SQLite** e executado em container **Docker**.

A página exibe cards com as tecnologias utilizadas e uma seção dinâmica que lista mensagens cadastradas pelo painel administrativo do Django.

---

## 🛠️ Tecnologias

| Tecnologia | Versão | Papel no projeto |
|---|---|---|
| Python | 3.12 | Linguagem base |
| Django | 5.1.3 | Framework web back-end |
| Tailwind CSS | CDN | Estilização via classes utilitárias |
| SQLite | — | Banco de dados local |
| Docker / Docker Compose | — | Containerização do ambiente |

---

## 📁 Estrutura do Projeto

```
demo-django/
├── core/                   # Pacote de configuração do projeto Django
│   ├── settings.py         # Configurações globais (INSTALLED_APPS, TEMPLATES, etc.)
│   ├── urls.py             # Roteador principal de URLs
│   ├── wsgi.py             # Ponto de entrada WSGI (produção)
│   └── asgi.py             # Ponto de entrada ASGI (produção)
├── home/                   # App responsável pela página principal
│   ├── migrations/         # Migrations geradas pelo Django
│   │   └── 0001_initial.py
│   ├── models.py           # Modelo Mensagem (título, conteúdo, data)
│   ├── views.py            # View index — busca mensagens e renderiza template
│   ├── urls.py             # Rotas do app home
│   └── admin.py            # Registro do modelo no painel admin
├── templates/
│   └── home/
│       └── index.html      # Template HTML com Tailwind CSS
├── Dockerfile              # Receita da imagem Docker
├── docker-compose.yml      # Orquestração do serviço web
├── requirements.txt        # Dependências Python
├── .gitignore
└── .dockerignore
```

---

## ⚙️ Como executar

### Pré-requisitos

- [Docker](https://docs.docker.com/get-docker/) instalado (inclui o `docker compose`)

Verifique com:

```bash
docker --version
docker compose version
```

### Passo a passo

**1. Clone o repositório e acesse o branch correto:**

```bash
git clone https://github.com/JoaoHPS06/demo-django.git
cd demo-django
git checkout bcc481-django-parte1
```

**2. Suba o container:**

```bash
docker compose up --build
```

Esse comando irá:
- Construir a imagem Docker com Python 3.12 e Django 5.1.3
- Aplicar as migrations e criar o banco SQLite
- Iniciar o servidor de desenvolvimento na porta 8000

**3. Acesse no navegador:**

- **Página principal:** http://localhost:8000  
- **Painel admin:** http://localhost:8000/admin/

**4. Para parar o servidor:**

```bash
# Ctrl+C no terminal, depois:
docker compose down
```

---

## 🗄️ Modelo de Dados

### `Mensagem` (`home/models.py`)

| Campo | Tipo Django | Descrição |
|---|---|---|
| `titulo` | `CharField(max_length=120)` | Título da mensagem |
| `conteudo` | `TextField` | Corpo da mensagem |
| `criada_em` | `DateTimeField(auto_now_add=True)` | Data/hora de criação (automática) |

- Ordenação padrão: mais recentes primeiro (`ordering = ["-criada_em"]`)
- Representação no admin: pelo campo `titulo`

---

## 🔗 Rotas

| URL | View | Descrição |
|---|---|---|
| `/` | `home.views.index` | Página principal com lista de mensagens |
| `/admin/` | Django Admin | Painel administrativo |

---

## 📸 Sistema em execução

### Página principal — sem mensagens cadastradas

> Exibição inicial ao subir o projeto pela primeira vez.

![Página principal sem mensagens](imagens/page-tutorial-django-parte1.png)

### Página principal — com mensagens cadastradas

> Após cadastrar mensagens pelo painel `/admin/`, elas aparecem listadas na seção "Mensagens do banco de dados".

<!-- Substitua pela sua captura de tela -->
![Página com mensagens](imagens/page-com-mensagens.png)

### Painel Admin — listagem de mensagens

> Interface administrativa gerada automaticamente pelo Django, com busca por título e conteúdo.

<!-- Substitua pela sua captura de tela -->
![Painel admin](imagens/admin-mensagens.png)

---

## 📌 Destaques da implementação

- **Docker como ambiente de desenvolvimento:** Python e Django rodam inteiramente dentro do container — sem instalação local das dependências.
- **Volume montado:** a pasta local é mapeada para `/app` no container, então alterações no código refletem imediatamente sem rebuild.
- **Tailwind via CDN:** sem pipeline de build (npm/Node), o CSS é carregado diretamente da CDN do Tailwind para simplificar o ambiente.
- **Django Admin configurado:** o modelo `Mensagem` é registrado com `list_display` e `search_fields` para facilitar o gerenciamento via painel.
- **Template com Django Template Language:** uso de `{% if %}`, `{% for %}` e filtros como `|date:"d/m/Y H:i"` para renderizar dados dinâmicos.

---

## 📚 Conceitos abordados neste roteiro

- Estrutura de projeto Django (`startproject`) e apps (`startapp`)
- Arquivo `Dockerfile` e `docker-compose.yml`
- `settings.py`: `INSTALLED_APPS`, `TEMPLATES`, `LANGUAGE_CODE`, `TIME_ZONE`
- Criação de modelo com `models.Model` e tipos de campo do Django ORM
- Registro no admin com `@admin.register`
- Views baseadas em função (FBV) e passagem de contexto para templates
- Roteamento com `urls.py` no app e inclusão em `core/urls.py`
- Template HTML com Django Template Language e Tailwind CSS
- Migrations: `makemigrations` e `migrate`
