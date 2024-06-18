# Docker for Laravel Applications

## Conceitos

## Docker compose

O Docker compose é uma forma de agregar diversos containers.

### Ficheiro `docker-compose.yaml`

**image**
Sempre que obter a imagem do Hub, deve ser indicada a imagem pretendida.

**build**
Em alternativa à **image**, o **build** obtém a imagem local.

**volume**
O volume relaciona pastas locais com as pastas do container.
A atualização é bi-direcional, ou seja, quando o container atualiza ficheiros 
dentro do container, as pastas locais são também atualizadas.
Em realidade é criada uma ponte entre as duas pastas.

## Processo

1. Criação do container para NGINX
2. Criação do container para MySQL
3. Criação do container para PHP
4. Criação do container para Composer
5. Criação da app Laravel

## 1. Criação do container para NGINX

### Passos

1. Criação da pasta /docker/nginx
2. Criação do ficheiro /docker/nginx/Dockerfile
3. Criação da imagem:

```
docker build --no-cache -t laravel-nginx .
```

4. Execução da imagem:

```
docker run --rm -p 8080:80 laravel-nginx
```

ou, especificando o volume na execução:

```
docker run -rm -p 8080:80 -v C:\Users\luciano\Source\Docker\laracast-docker-tutorial\docker\nginx\src:/var/www/public_html/public laravel-nginx
```

### Teste

1. Criação da pasta /docker/src
2. Criação do ficheiro /docker/src/index.html

### Docker compose

1. Criação do ficheiro /docker-compose.yaml
2. No ficheiro /docker-compose.yaml espeficiar o **build** com 
   *contexto* /docker/nginx e *dockerfile* Dockerfile

## 2. Criação do container para MySQL

### Passos

1. Criação da pasta /docker/mysql
2. Criação do ficheiro /docker/mysql/Dockerfile

### Atualização do Docker compose

1. Atualização do ficheiro /docker-compose.yaml
2. No ficheiro /docker-compose.yaml espeficiar o **build** com 
   *contexto* /docker/mysql e *dockerfile* Dockerfile

## 3. Criação do container para PHP

### Passos

1. Criação da pasta /docker/php
2. Criação do ficheiro /docker/php/Dockerfile

### Teste

1. Criação do ficheiro /docker/src/index.php

### Atualização do Docker compose

1. Atualização do ficheiro /docker-compose.yaml
2. No ficheiro /docker-compose.yaml espeficiar o **build** com 
   *contexto* /docker/php e *dockerfile* Dockerfile

## 4. Criação do container para Composer

### Passos

1. Criação da pasta /docker/composer
2. Criação do ficheiro /docker/composer/Dockerfile

### Atualização do Docker compose

1. Atualização do ficheiro /docker-compose.yaml
2. No ficheiro /docker-compose.yaml espeficiar o **build** com 
   *contexto* /docker/composer e *dockerfile* Dockerfile
3. Criação da imagem:

```
docker-compose build composer
```

## 5. Criação da app Laravel

1. Criação da app Laravel através do composer do Docker:

```
docker-compose run --rm composer create-project laravel/laravel .
```

Note que ao executar o **composer**, o Docker entende que o workdir é o `/docker/src`.

## Deploy

### Certificados

[Install MKCert on Windows|Linux](https://thriveread.com/mkcert-localhost-ssl-certificates/)

[Locally trusted development certificates with mkcert and IIS](https://medium.com/@aweber01/locally-trusted-development-certificates-with-mkcert-and-iis-e09410d92031)

[MKCERT on Github](https://github.com/FiloSottile/mkcert#windows)

```
docker-compose -f docker-compose.yml -f docker-compose.prod.yml up --build nginx
```

```
docker-compose run --rm php -i | grep opcache
```
