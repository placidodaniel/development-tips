# development-tips - Dicas úteis que fui coletando para auxiliar no dev.

# NodeJS

## Criando aplicação com nodejs:

1. Cria o arquivo package.json -> Guarda as dependências do projeto em package.json
```bash
> npm init -y 
```
2. Cria primeira dependência. Express é um microframework que trata rodas e views
```bash
> npm install express  
```
3. Executar a aplicação, criando um servidor.
```bash
> node server.js
```
4. Dependencia de desenvolvimento -D, nodemon faz que não precise reiniciar o server cada vez que altera ele, por isso a dependência de desenvolvimento
```bash
> npm install -D nodemon 
```
5. Criado em package.json uma dependencia que só roda em dev, e criada a tag "dev" em "scripts"
```bash
> npm run dev 
```

# Docker

## Instalando o Mongo por meio do docker e utilizando no NodeJs

1. Baixa a ultima versão do mongodb
```bash
> docker pull mongo
```
2. Configurando container para rodar na porta 27017 (Porta Local : Porta do Container) com o nome 'mongodb'
`--name` = nome da container que esta sendo criado
`-p` = redirecionamento de porta, toda a vez que acessar a porta 27017 da minha maquina acessa a porta 27017 mongodb
`-d` = qual imagem se deseja utilizar (No caso baixamos a imagem do mongo)
```bash
> docker run --name mongodb -p 27017:27017 -d mongo
```
3. Testando se os container foram criados com sucesso. 
O comando abaixo retorna todas as imagens do docker, inclusive as que estão paradas
```bash
> docker ps -a 
```
4. Para iniciar ou parar um container bastar usar os seguintes comandos respectivamente:
```bash
> docker start 'nomecontainer'
> docker stop 'nomecontainer'
```
5. Para testar o mongo, basta ir em https://robomongo.org/ e fazer download do robo3t.
6. Instalando dependencia no projeto NodeJs para conectar o mongodb
```bash
> npm install mongoose 
```
7. Faz o papel do require em um diretorio em todos os arquivos automaticamente. Muito útil
```bash
> npm install require-dir 
```
8. Modulo para paginar registros do mongo
```bash
> npm install mongoose-paginate  
```
9. Modulo de autenticação no mongo
```bash
npm install cors
```

------------------------------
ReactJS - APlicações SIstemas

https://yarnpkg.com/ - Ferramenta parecida com npm para gestão de pacotes mais veloz.

Criando uma aplicação reactenative. Também resolve os problemas por navegadores que não suportam nvoas configurações de scripts
npm install -g create-react-app

create-react-app huntweb //Da um nome para o projeto criado chamado huntweb

Startar aplicação: npm start

//Biblioteca para acessar uma api do react native para o backend
yarn add axios

//Adiciona biblioteca para trabalhar com rotas
yarn add react-router-dom
------------------------------------------------------------------
Criando uma rede entre dois conteiners no docker.
Fonte: https://medium.com/@renato.groffe/postgresql-docker-executando-uma-inst%C3%A2ncia-e-o-pgadmin-4-a-partir-de-containers-ad783e85b1a4


docker network create --driver bridge postgres-network

docker run --name rede-postgres --network=postgres-network -e "POSTGRES_PASSWORD=Postgres2018!" -p 5432:5432 -v E:\Users\daniel\apps\sao-jose\db:/var/lib/postgresql/data -d postgres
- O atributo name especifica o nome do container a ser gerado (teste-postgres);
- Para o atributo network foi definido o valor da rede criada na seção anterior (postgres-network);
- No atributo POSTGRES_PASSWORD foi indicada a senha do administrador (para o usuário default postgres);
- O atributo -p indica a porta (5432) em que se dará a comunicação com o PostgreSQL, a qual será mapeada para a porta default (5432) deste SGBD dentro do container;
- Através do atributo -v foi criado um volume, especificando assim o diretório no Ubuntu Desktop em que serão gravados os arquivos de dados (E:\Users\daniel\apps\sao-jose\db);
- Quanto ao atributo -d, este parâmetro determina que o container em questão será executado como um serviço em background;
- Temos indicada ainda a imagem utilizada como base para a geração do container (postgres).

docker run --name pgadmindb --network=postgres-network -p 15432:80 -e "PGADMIN_DEFAULT_EMAIL=phpsistemas@gmail.com" -e "PGADMIN_DEFAULT_PASSWORD=PgAdmin2018!" -d dpage/pgadmin4
- O atributo name indica o nome do container a ser criado (teste-pgadmin);
- No atributo network foi atribuído o nome da rede utilizada na comunicação entre a instância do PostgreSQL e o pgAdmin (postgres-network);
- O atributo -p especifica a porta (15432) em que acontecerá a comunicação com o pgAdmin 4, a qual será mapeada para a porta default (80) desta aplicação Web;
- No atributo PGADMIN_DEFAULT_EMAIL foi informado o e-mail de acesso ao pgAdmin;
- No atributo PGADMIN_DEFAULT_PASSWORD foi indicada ainda a senha de acesso ao pgAdmin 4;
- Temos especificada também a imagem empregada na geração do container (dpage/pgadmin4).

postgresql://[user[:password]@][netloc][:port][/dbname][?param1=value1&...]

Here are examples from same document

postgresql://
postgresql://localhost
postgresql://localhost:5432
postgresql://localhost/mydb
postgresql://user@localhost
postgresql://user:secret@localhost
postgresql://other@localhost/otherdb?connect_timeout=10&application_name=myapp
postgresql://localhost/mydb?user=other&password=secret
