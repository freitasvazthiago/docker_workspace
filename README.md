# Ambiente docker 

[logo]:https://cdn.cloudlabs.com.br/wp-content/uploads/2017/07/whale-docker-logo.png
[redis]:https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQnIXOPDonZhJdI2xnT0fRIf3RiYZFzUSKK0yO-f7UVg7KujlX_
[mssql]:https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQvAPhBHr4xbPDhD_uQUkOw47tUtM4jqRN69xTdZmW8NtgsfzB3
[nginx]:https://2bjee8bvp8y263sjpl3xui1a-wpengine.netdna-ssl.com/wp-content/uploads/NGINX.png
[php]:https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSMCrXx7hks2jNSC__-tJ791WR2j8hEhytnErf82s2SxRkU_8hg

## Requisitos

- Git
- Docker ([Download](https://www.docker.com/community-edition#/download))
- Docker Compose ([Download](https://docs.docker.com/compose/install/#install-compose))

## Plataformas homologadas

### Documentação:

[win]:https://docs.docker.com/images/windows_48.svg
[apple]:https://docs.docker.com/images/apple_48.svg
[lin]:https://docs.docker.com/images/linux_48.svg

- ![Win][win][Windows](https://docs.docker.com/docker-for-windows/)
- ![Apple][apple][Apple](https://docs.docker.com/docker-for-mac/)
- ![Lin][Lin][Linux](https://docs.docker.com/engine/installation/linux/ubuntu/)

## Instalação

1 - Clone o repositório na mesma estrutura dos projetos.

`git clone` 

A estrutura deve estar assim:
```
+ ex-projeto
+ ex2-projeto
```
2 - Na pasta ./ e copie renomeie os arquivos:  

- docker-compose.yml.example -> docker-compose.yml
    * incluir em `nginx` -> `ports` as seguintes linhas:
      - "8000:8000"

3 - Na pasta ./nginx/sites e copie renomeie os arquivos:  

- default.conf.example (altere o parametro `listen` para `8000`)

4 - Adicione os seguintes dominios no arquivo de hosts.

- Linux - /etc/hosts
- Windows - c:\Windows\System32\drivers\etc\hosts

```
127.0.0.1  nginx
```

## Iniciar os containers

1 - Copie e renomeie o arquivo que esta dentro da raiz do projeto.

- env-example -> .env

2 - Execute os seguintes comandos:

`docker login` (este comando só precisa ser executado uma vez)

2.1 - Baixar as imagens base (Somente para usuários windows)

`docker push usuario/repositorio`

Obs.: Caso receba o erro "no route to host" verifique se não há nenhum container em execução com o comando `docker ps` e execute o comando `docker network prune` 

3 - Subir o serviço

`docker-compose up -d`

## Teste

Acesse as seguintes urls para confirmar:

`nginx:8000` -> PROJETO

Checar se as portas foram expostas corretamento pelo Docker:

- Linux
 
`netstat -atunp | grep 8000`

- Windows (CMD)

`netstat -n | find "3000"`  
`netstat -n | find "8000"`