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
> docker run --name rede-postgres -e "POSTGRES_PASSWORD=Postgres2020!" -itd --shm-size=1g -p 5432:5432 -v E:\Users\daniel\apps\postgres\db:/var/lib/postgresql/data -d postgres
```
- O atributo `name` especifica o nome do container a ser gerado (teste-postgres);
- No atributo `POSTGRES_PASSWORD` foi indicada a senha do administrador (para o usuário default postgres);
- O atributo `-p` indica a porta (5432) em que se dará a comunicação com o PostgreSQL, a qual será mapeada para a porta default (5432) deste SGBD dentro do container, ou seja, porta externa(localhost) para porta interna (Dentro do container);
- Através do atributo `-v` foi criado um volume, especificando assim o diretório no Ubuntu Desktop em que serão gravados os arquivos de dados (E:\Users\daniel\apps\postgres\db);
- Quanto ao atributo `-d`, este parâmetro determina que o container em questão será executado como um serviço em background;
- Temos indicada ainda a imagem utilizada como base para a geração do container (postgres).

# Linux
## Configurando servidor Linux do Zero
1. Acesse o servidor com o usuário root e crie um usuário. Por exemplo usuário deploy.
```bash
adduser deploy 
```
2. Dando permissão de sudo para o usuário deploy. 
```bash
usermod -aG sudo deploy
```
3. Configurando sua chave SSH em sua máquina para acessar o servidor linux por meio do terminal linux:
```bash
ssh-keygen -t rsa
```
Depois de inserir este comando, algumas novas perguntas aparecerão:

Insira o arquivo no qual deseja salvar a chave (/home/user/.ssh/id_rsa):

Geralmente, recomenda-se simplesmente deixá-lo como está (pressione ENTER sem digitar nada) para que o gerador de chaves possa criar o par de chaves no local padrão (neste tutorial eu inseri um nome diferente tut_id para evitar chaves duplicadas, (o dispositivo já tinha um id_rsa chaves geradas). As duas primeiras perguntas que aparecerão:

Introduza a frase de acesso (empty for no passphrase). Então introduza a mesma frase novamente.

Agora por razões de conveniência, eu gosto de deixar os vazios também. Dessa forma, depois de definir as teclas para cima com o seu servidor remoto, você não precisará usar qualquer tipo de senha para o login. Você simplesmente digita o comando ssh user@serverip e ele irá fazer o login enquanto as chaves são corretamente configuradas. Mas se você precisar de mais segurança, digite uma frase-senha nesta seção. Se escolher esta opção, terá de introduzir a palavra-passe sempre que ligar ao dispositivo remoto.

IMPORTANTE! Existem duas chaves criadas aqui (PRIVATE e PUBLIC): tut_id e tut_id.pub (no seu caso, deve ser id_rsa e id_rsa.pub). Tome muito cuidado com o arquivo chamado id_rsa (esta é a chave PRIVATE), tenha apenas em seu dispositivo local e não dê a NINGUÉM.
4. Copiando a chave pública para o servidor remoto
Depois de gerar o par de chaves RSA, temos que colocar nossa chave pública no servidor virtual remoto.
Há um comando simples que colocará sua chave pública diretamente no arquivo do authorized_keys do servidor remoto (este arquivo mantém todas as chaves públicas:
```bash
ssh-copy-id user@serverip
```
5. Configurando permissões (no servidor com o usuário deploy).
Na pasta /home/user/.ssh de as permissões da seguinte forma:
```bash
chmod 600 authorized_keys 
cd ..
chmod 700 .ssh
```
6. Instalando o docker no Linux. Realizar este comando com o usuário deploy.
```bash
sudo apt install docker.io
```
7. Dando permissão para o usuário deploy trabalhar com o docker. Realizar este comando com o usuário deploy.
```bash
usermod -aG docker deploy 
```
8. Criando máquina docker postgresdb com o nome 'database' (Guarde a senha passada e nunca utilize ela)
```bash
docker run --name database -e POSTGRES_PASSWORD=senha -p 17863:5432 -v /docker/postgresql:/var/lib/postgresql/data --restart always -d -itd --shm-size=1g postgres
```
9. Acessando máquina docker criada, criando primeiro banco de dados e configurando usuario para o banco. 
```bash
docker exec -it database /bin/bash
su postgres
psql
CREATE DATABASE empresas;
CREATE USER appemp WITH ENCRYPTED PASSWORD='senha';
GRANT ALL PRIVILEGES ON DATABASE empresas TO appemp;
```
9.1 Permitindo função 'unaccent' no database Postgres:
Acessando a máquina onde o postgres esta instalado, executar o seguinte comando:
```bash
psql
\c database //Conectando o database que se deseja instalar a função
CREATE EXTENSION unaccent;
```

10. Se necessário copiar arquivos do servidor para a máquina docker. Duvidas, documentação do docker.
```bash
docker cp /home/deploy/file.csv database:/dados/file.csv
```
11. Se necessário copiar arquivos de sua máquina para o servidor: 
```bash
rsync -avzP -e 'ssh -p22' arquivo.csv deploy@ipservidor:/home/deploy
```
12. Instalando o PM2:
O PM2 é um gerenciador de processos para nodejs. 
Para instalar, basta:
```bash
sudo npm install -g pm2
```
Pegar o endereço bin do node:
```bash
npm global bin
```
Editar o arquivo de inicialização do Linux 
```bash
vim ~/.bashrc
```
Adicione o código abaixo na última linha do script:
```bash
export PATH="$(npm bin):$PATH"
```
Rodar a alteração salva
```bash
source ~/.bashrc
```
Abaixo Segue os comandos para rodar para que sempre que o servidor reiniciar, o PM2 reinicie juntamente com o servidor.
```bash
pm2 startup ubuntu -u deploy
sudo env PATH=$PATH:/usr/bin pm2 startup ubuntu -u deploy --hp /home/deploy
```
13. Inslando o NGINX
O NGINX é um servidor de proxy reverso. Ele serve para redirecionar um endereço para um local ou porta especifico. 
Para instalar, com o usuário root: 
```bash
apt install nginx
cd /etc/nginx/sites-available/
```
Configuração Padrão NGINX
```bash
server {
  server_name testdeploy.rocketseat.com.br;

  location / {
    proxy_pass http://127.0.0.1:3333;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_cache_bypass $http_upgrade;
  }
}
```
14.Instalando um certificado SSL Gratuito:
Acessar o site: https://letsencrypt.org/ e o site https://certbot.eff.org/ em outra aba.

Informe o servidor e o sistema operacional (NGINX e UBUNTU Versão)

15. Instalando o redis com docker 
--appendonly yes: Configuração para redis persistente. 
```bash
sudo docker run --restart=always -p 6379:6379 -v /docker/redis:/data --name redis -d redis redis-server --requirepass Redis2019! --appendonly yes 
```
16. Instalando o apenas o redis-cli no seu Linux
```bash
sudo apt-get install redis-tools
```
17. Instalando o wordpress com mysql, via docker-compose:
- Crie o arquivo docker-compose.yml conforme exemplo abaixo:
```bash
version: '2'
services:
   db:
     image: mysql:latest
     volumes:
       - /home/user/docker/mysql:/var/lib/mysql
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: somewordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress

   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     ports:
       - "8000:80"
     restart: always
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_USER: wordpress
       WORDPRESS_DB_PASSWORD: wordpress
```
- Salve arquivo, depois, no diretório onde foi criado, digite o comando:
```
docker-compose up -d
```
Pronto!!!

https://www.youtube.com/watch?v=ICIz5dE3Xfg

## Resolvendo problema com "pq: could not resize shared memory segment. No space left on device" no postgre:
https://medium.com/@shanikanishadhi1992/how-to-resolve-error-could-not-resize-shared-memory-segment-postgresql-no-space-left-on-device-8344c0ed3272

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
# git

## Para clonar um repositório:
```bash
git clone git clone <url-do-repositorio-do-projeto>
```
## Para clonar um branch especifico
```bash
git clone -b minhaBranch git@github.com:user/myproject.git
```
## Para alternar para um branch especifico:
```bash
git checkout -b <nome-do-seu-branch-local> origin/<nome-do-branch-remoto>
```
## Para criar um branch local
```bash
git checkout -b <nome-do-seu-branch-local>
```
## Para atualizar um repositório já existente para outro novo:
Remova a pasta .git do diretório principal do repostório, em seguida, execute os seguintes comandos.
```bash
git init
git remote add origin https://github.com/placidodaniel/REPOSITORIO.git
git add .
git commit -m "first commit"
git branch -M main
git push -u origin main
```
# heroku

## Como fazer deploy de uma aplicação com node no heroku:

Caso queriam estudar como fazer uma plublicação de uma aplicação desenvolvida com nodejs, basta seguir a explicação abaixo:

https://devcenter.heroku.com/articles/getting-started-with-nodejs

## scale aplication heroku:
```bash
heroku ps:scale web=0 
heroku ps:scale web=1 
```
# Rabbitmq
## Como habilitar os módulos do rabbit, permitindo console de administração.
Para instalar via docker:

```bash
mkdir -p /docker/rabbitmq/data
docker run -d --name rabbitmq  -p 5672:5672  -p 15672:15672  --restart=always  --hostname rabbitmq-master  -v /docker/rabbitmq/data:/var/lib/rabbitmq  rabbitmq
docker exec -it rabbitmq /bin/bash
rabbitmq-plugins enable rabbitmq_management
rabbitmq-plugins enable rabbitmq_shovel rabbitmq_shovel_management
```
Instalando Versão com gerenciador web
```bash
docker run -d --name rabbitmq -p 2672:5672 -p 25672:15672 --restart=always --hostname rabbitmq-master -v /docker/rabbitmq/data:/var/lib/rabbitmq rabbitmq:3-management
```

# PHP com Laravel
1. Instalando o php no Ubuntu:
```bash
sudo apt install php
sudo apt install phpunit
```
2. Instalando o composer no Ubuntu:
```bash
curl -sS https://getcomposer.org/installer -o composer-setup.php
HASH=`curl -sS https://composer.github.io/installer.sig`
echo $HASH #conferir se o hash bate com o site do composer, evitando possíveis versões hackeadas ou corrompidas
php -r "if (hash_file('SHA384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" 
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
composer #testar se esta executando o composer via comando.
```
3. Criando um projeto com Laravel no Ubuntu, setando uma versão especifica:
```bash
composer create-project --prefer-dist laravel/laravel:^7.0 nome-projeto
```
4. Entendendo o projeto do Laravel.

4.1. Pasta `app` é onde tudo acontece;

4.1.1. Pasta `middleware` é a funcionalidade que fica entre o backend e o frontend, podem ser feitas validações aqui, como validações de acesso;

4.1.2. Pasta `controllers` é onde ficam os controllers do projeto;

4.2. Pasta `resources` é onde ficam as `views` do projeto;
4.2.1. O `blade` é uma ferramenta para escrever o PHP na página do frontend. Facilita muito para utilização por meio de designers escreverem o código HTML junto com as rotinas de desenvolvimento.

4.3. 

5. Rodando o projeto em Laravel.
Dentro do diretório do projeto, execute o seguinte comando:
```bash
php artisan serve
```
6. Rotas no Laravel:
As rotas são configuradas no diretório `routes`.
6.1. Arquivo `api.php` configura as rotas de api, exemplo: APIs do Google.
6.2. Arquivo `web.php` configura as rotas de endereços web. Exemplo: Site de usuários



## Tenho Dúvidas... O que Faço?! ❓

Caso tenham dúvidas ou sugerirem dicas ou correções, sintam-se a vontade em abrir uma **[ISSUE AQUI](https://github.com/infolouco/development-tips/issues)**. Assim que possível, estarei respondendo as todas as dúvidas que tiverem!
