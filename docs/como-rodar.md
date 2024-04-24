# Rodando o projeto
> This is the second page


## Configurando o Docker

#### MySQL
- Primeiro precisamos criar um container para o MySQL para subirmos um banco de dados utilizável pela aplicação, para isso rode o seguinte comando na pasta raiz do projeto

````bash
    docker volume create mysql
````

````bash
    docker network create mysql
````

````bash
    docker run -d --name mysql -e MYSQL_ROOT_PASSWORD=strong_password -v mysql --network mysql -p 3306:3306 mysql:8.0
````

- Finalmente, seu container do MySQL está configurado e para executá-lo você pode rodar o seguinte comando:
````bash
    docker start mysql
````

- Além disso, precisamos criar o nosso banco de dados dentro do container do MySQL
````bash
    docker exec mysql mysql -u root -pstrong_password -e "create database website"
````
#### Aplicação
- Agora podemos rodar o docker compose para subirmos a docker image da Intranet
````bash
  docker-compose up -d
````
## Configurando variáveis de ambiente
- Copie o arquivo .env.example localizado na pasta root do projeto e a nomeie como .env
  Você pode fazer isso através do código abaixo
````bash
    cp .env.example .env
````
- Dentro do `.env` atribua o valor `1000` às variáveis de ambiente `WWWGROUP` e `WWWUSER` como ilustrado abaixo:
````bash
    WWWGROUP=1000
    WWWUSER=1000
````
- Gere uma chave para que a variável `APP_KEY` seja preenchida
````bash
    sail artisan key:generate
````
Sua variável ficará assim:
`
 APP_KEY=base64:1m2dlkvIHyEwdEO1JwxE6SRxjVCHqSaIziFtj+BBSKE=
`
- Por último, podemos configurar uma `APP_URL` para o projeto
Em desenvolvimento local, botaremos: `APP_URL=localhost`
## Baixando as dependências do projeto
- Primeiro vamos baixar as dependências do nosso projeto Laravel no container, para o fazer 
````bash
    docker-compose exec intranet composer install
````
- Também temos dependências JavaScript que precisamos baixar, para isso rodaremos:

````bash
    sail npm run dev
````
## Executando
- Enfim, podemos rodar o projeto, que rodará através do seguinte comando:
````bash
    sail npm run dev
````
>O sail é uma ferramenta que prepara o ambiente para desenvolvimento PHP utilizando Docker, ele estará disponível para uso a partir do momento em que instalamos o composer no container da Intranet