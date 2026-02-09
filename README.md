# Docker - FastAPI

Este trabalho envolve tarefa prática da EBAC no que diz respeito a criar container para inicialização de FastAPI com Docker.

## Arquivos do Projeto

Este repositório contém:

* **`Dockerfile`**: Detalha a construção da imagem Docker, incluindo a instalação do Poetry e das dependências do projeto
* **`docker-compose.yml`**: Configura o ambiente Docker Compose com mapeamento de portas, volumes para sincronização de código e variáveis de ambiente
* **`main.py`**: Código-fonte da aplicação FastAPI com endpoints CRUD para gerenciamento de livros
* **`pyproject.toml`**: Arquivo de configuração do Poetry listando todas as dependências
* **`poetry.lock`**: Garante consistência das versões de dependências entre ambientes
* **`.env`**: Variáveis de ambiente (configuração de banco de dados e autenticação)
* **`.gitignore`**: Arquivos ignorados pelo Git
* **`.dockerignore`**: Arquivos ignorados pelo Docker

## Pré-requisitos

* Docker
* Docker Compose

## Clone do Repositório
```bash
git clone https://github.com/savifb/dockerFastapi.git
cd dockerFastapi
```

## Configuração

Crie o arquivo `.env` com as variáveis de ambiente:
```bash
cp .env.example .env
```

Edite o `.env` conforme necessário.

## Rodando a Aplicação

Inicie os contêineres em segundo plano:
```bash
docker-compose up --build -d
```

A aplicação estará disponível em:
* http://localhost:8000
* http://localhost:8000/docs (documentação interativa)

## Parando a Aplicação

Para parar os contêineres:
```bash
docker-compose down
```

## Autenticação

A API usa HTTP Basic Authentication. Configure as credenciais no arquivo `.env`:
```env
MEU_USUARIO=seu_usuario
MINHA_SENHA=sua_senha
```

## Endpoints

### Público
* `GET /` - Mensagem de boas-vindas

### Autenticados
* `GET /livros?page=1&limit=10` - Lista livros (paginado)
* `POST /adiciona` - Adiciona novo livro
* `PUT /atualiza/{id_livro}` - Atualiza livro existente
* `DELETE /delete/{id_livro}` - Remove livro

## Banco de Dados

O projeto usa SQLite. O arquivo `livros.db` é criado automaticamente na primeira execução.

Para resetar o banco:
```bash
docker-compose down
rm livros.db
docker-compose up -d
```

## Estrutura do Projeto
```
dockerFastapi/
├── .dockerignore
├── .gitignore
├── Dockerfile
├── README.md
├── docker-compose.yml
├── livros.db
├── main.py
├── poetry.lock
└── pyproject.toml
```
