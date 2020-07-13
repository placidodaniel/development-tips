# development-tips - Dicas úteis que fui coletando para auxiliar no dev.
Fique a vontade para contribuir!

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

# Python

## Como alterar a versão padrão do Python no Linux

1. Se você tem mais de uma versão do python instalada no Linux e quer ter uma padrão ou precisa ficar mudando, basta utilizar o comando abaixo de acordo com a versão que você deseja:
```bash
> sudo ln -sf /usr/bin/python3.6 /usr/bin/python
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
## Vendo os logs de um container do docker
1. no terminal (Windows ou Linux) execute o seguinte comando: 
```bash
> docker logs -f --tail=100 nomedocontainer 
```
`-f` = fica escutando o arquivo de logs. 

`--tail=100` = Mostra os 100 últimos registros de logs.
## Vendo o volume configurado de um container do docker
1. no terminal (Windows ou Linux) execute o seguinte comando: 
```bash
> docker volume inspect nomedocontainer 
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
# Dias úteis ⭐️

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

# Linux

## Resolvendo problemas de pacotes quebrados. 
1. Se você já tentou de tudo e não conseguiu resolver seu problema com pacotes quebrados no linux, utilize o comando abaixo, removendo os pacotes recursivamente (Do último para o primeiro em termos de dependência).
```bash
sudo dpkg --remove --force-remove-reinstreq nome_pacote
sudo apt update
```

## Reduzindo tamanho de um PDF por meio do GS do linux
```bash
sudo apt install ghostscript
```
```bash
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/prepress -dNOPAUSE -dQUIET -dBATCH -sOutputFile=compressed_PDF_file.pdf input_PDF_file.pdf
```

dPDFSETTINGS	Description
/prepress (default)	Higher quality output (300 dpi) but bigger size
/ebook	Medium quality output (150 dpi) with moderate output file size
/screen	Lower quality output (72 dpi) but smallest possible output file size

# Ambiente de desenvolvimento java no Visual Studio. 
1. Instale os seguintes aplicativos.

git 
https://git-scm.com/download/win

node
https://nodejs.org/en/

jdk
https://www.oracle.com/technetwork/ja...

Visual Studio Code
https://code.visualstudio.com/

Visual Studio Code Extensions

https://www.youtube.com/redirect?v=vDCGeZehtQg&event=video_description&q=https%3A%2F%2Fblog.bitsrc.io%2Ftop-10-vs-code-extensions-for-frontend-developers-in-2018-7992282db2ca&redir_token=NtqaCMhqeQQlZV7Brxn30l7tSx98MTU5MDQxMjgyOEAxNTkwMzI2NDI4

https://www.youtube.com/redirect?v=vDCGeZehtQg&event=video_description&q=https%3A%2F%2Fonextrapixel.com%2Fbest-visual-studio-code-extensions%2F&redir_token=NtqaCMhqeQQlZV7Brxn30l7tSx98MTU5MDQxMjgyOEAxNTkwMzI2NDI4]

# heroku

## Como fazer deploy de uma aplicação com node no heroku:

Caso queriam estudar como fazer uma plublicação de uma aplicação desenvolvida com nodejs, basta seguir a explicação abaixo:

https://devcenter.heroku.com/articles/getting-started-with-nodejs

## scale aplication heroku:
```bash
heroku ps:scale web=0 
heroku ps:scale web=1 
```

## Tenho Dúvidas... O que Faço?! ❓

Caso tenham dúvidas ou sugerirem dicas ou correções, sintam-se a vontade em abrir uma **[ISSUE AQUI](https://github.com/infolouco/development-tips/issues)**. Assim que possível, estarei respondendo as todas as dúvidas que tiverem!
