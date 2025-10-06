SIPUBTECH Movies Challenge
Este projeto implementa uma API REST para gestão de filmes (CRUD) utilizando uma arquitetura de microserviços em Go. A comunicação interna é feita via gRPC/Protobuf, e a persistência de dados utiliza MongoDB.

🚀 Tecnologias
Linguagem: Go

Banco de Dados: MongoDB

Containers: Docker e Docker Compose

Comunicação Inter-serviço: gRPC com Protocol Buffers

Arquitetura: Hexagonal (Ports & Adapters)

Documentação: Swagger

⚙️ Arquitetura de Microserviços
O projeto é estruturado em três containers principais, orquestrados via Docker Compose:

API Gateway: Ponto de entrada REST, responsável por receber requisições HTTP e rotear a comunicação via gRPC.

Movies Service: Microserviço principal que contém a lógica de negócio (CRUD) e se comunica com o MongoDB.

MongoDB: Banco de dados para persistência dos dados de filmes.

▶️ Como Inicializar a Aplicação
A inicialização do stack completo (API Gateway, Movies Service e MongoDB) é feita com um único comando na raiz do projeto:

Bash

docker compose up -d --build
Observação: O serviço movies será inicializado e fará a carga inicial dos dados do arquivo movies.json no MongoDB.

A API estará acessível em: http://localhost:8080

📖 Documentação da API (Swagger)
A documentação interativa da API, gerada via Swagger, estará disponível no seguinte endereço após a inicialização:

http://localhost:8080/swagger/index.html
🧭 Rotas e Exemplos de Uso (CRUD)
A API expõe as seguintes rotas na porta 8080:

Método	Rota	Descrição
GET	/movies	Retorna a lista de todos os filmes.
GET	/movies/{id}	Retorna um filme específico por ID.
POST	/movies	Cria um novo filme.
DELETE	/movies/{id}	Remove um filme por ID.

Export to Sheets
Exemplos via cURL
Você pode usar o ID do filme inserido a partir do movies.json (Ex: 60f0c0b8b8b8b8b8b8b8b8b8).

1. GET (Todos os Filmes)
Bash

curl -X GET "http://localhost:8080/movies"
2. POST (Criar Novo Filme)
Bash

curl -X POST "http://localhost:8080/movies" \
     -H "Content-Type: application/json" \
     -d '{
           "title": "O Senhor dos Anéis",
           "director": "Peter Jackson",
           "year": 2001
         }'
3. GET (Filme por ID)
(Use o ID retornado na criação ou de um filme existente)

Bash

curl -X GET "http://localhost:8080/movies/{id_do_filme}"
4. DELETE (Filme por ID)
Bash

curl -X DELETE "http://localhost:8080/movies/{id_do_filme}"
✅ Testes Unitários
Os testes unitários foram implementados no serviço Movies seguindo os princípios da Arquitetura Hexagonal, cobrindo:

Testes de unidade (sem mocks) para a camada de core/domain.

Testes de integração (com mocks) para isolar a lógica de negócio das dependências externas (como o MongoDB).

Para rodar os testes, execute na pasta do serviço Movies:

Bash

go test ./...
