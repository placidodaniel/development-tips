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
2. Configurando container para rodar na porta 27017 (Porta Local : Porta do Container) com o nome 'mongodb'. Veja os parâmetros utilizados abaixo no comando `docker run`:

`--name` = nome da container que esta sendo criado.

`-p` = redirecionamento de porta, toda a vez que acessar a porta 27017 da minha maquina acessa a porta 27017 mongodb.

`-d` = qual imagem se deseja utilizar (No caso baixamos a imagem do mongo).
```bash
> docker run --name mongodb -p 27017:27017 -d mongo
```
3. Testando se os container foram criados com sucesso. 
O comando abaixo retorna todas as imagens do docker, inclusive as que estão paradas:
```bash
> docker ps -a 
```
4. Para iniciar ou parar um container bastar usar os seguintes comandos respectivamente:
```bash
> docker start 'nomecontainer'
> docker stop 'nomecontainer'
```
5. Para testar o mongo, basta ir em https://robomongo.org/ e fazer download do robo3t.
6. Instalando dependencia no projeto NodeJs para conectar o mongodb:
```bash
> npm install mongoose 
```
7. Faz o papel do require em um diretorio em todos os arquivos automaticamente. Muito útil:
```bash
> npm install require-dir 
```
8. Modulo para paginar registros do mongo:
```bash
> npm install mongoose-paginate  
```
9. Modulo de autenticação no mongo:
```bash
> npm install cors
```
## Acessando terminal container do docker 
1. no terminal (Windows ou Linux) execute o seguinte comando: 
```bash
> docker exec -it nomedocontainer bash
```
## Copiando arquivo ou diretorio do container para maquina local no docker:
1. no terminal (Windows ou Linux) execute o seguinte comando: 
- Copiando Diretório Completo
```bash
docker cp nomeimagem:/home/repositorioRemoto /home/repositorioLocal
```
- Copiando Arquivo
```bash
docker cp nomeimagem:/home/arquivoRemoto.csv /home/repositorioLocal
```
# Dias úteis

## https://yarnpkg.com/ - Ferramenta parecida com npm para gestão de pacotes mais veloz.

# ReactJS
1. Criando uma aplicação reactenative. Também resolve os problemas por navegadores que não suportam novas alterações no versionamento do javascript.
```bash
> npm install -g create-react-app
```
2. Da um nome para o projeto criado chamado 'nomeprojeto'. Utilizar sem aspas:
```bash
> create-react-app 'nomeprojeto' 
```
3. Startar aplicação:
```bash
> npm start
```
4. Biblioteca para acessar uma api do react native para o backend:
```bash
> yarn add axios
```
5. Adiciona biblioteca para trabalhar com rotas
```bash
> yarn add react-router-dom
```
# Configurando postgres com docker, entendendo todos os parâmetros que são passados ao container docker com a imagem do postgres. 
```bash
> docker run --name rede-postgres -e "POSTGRES_PASSWORD=Postgres2020!" -p 5432:5432 -v E:\Users\daniel\apps\postgres\db:/var/lib/postgresql/data -d postgres
```
- O atributo `name` especifica o nome do container a ser gerado (teste-postgres);
- No atributo `POSTGRES_PASSWORD` foi indicada a senha do administrador (para o usuário default postgres);
- O atributo `-p` indica a porta (5432) em que se dará a comunicação com o PostgreSQL, a qual será mapeada para a porta default (5432) deste SGBD dentro do container, ou seja, porta externa(localhost) para porta interna (Dentro do container);
- Através do atributo `-v` foi criado um volume, especificando assim o diretório no Ubuntu Desktop em que serão gravados os arquivos de dados (E:\Users\daniel\apps\postgres\db);
- Quanto ao atributo `-d`, este parâmetro determina que o container em questão será executado como um serviço em background;
- Temos indicada ainda a imagem utilizada como base para a geração do container (postgres).