# Ambiente docker para aplicações PHP

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
`git clone`  
`git clone`

A estrutura deve estar assim:
```
+ sisa-docker
+ sisa-banco-sangue
```
2 - Na pasta ./ e copie renomeie os arquivos:  

- docker-compose.yml.example -> docker-compose.yml
    * incluir em `nginx` -> `ports` as seguintes linhas:
      - "3000:3000"
      - "8000:8000"

3 - Na pasta ./nginx/sites e copie renomeie os arquivos:  

- laravel.conf.example -> api.conf  (altere o parametro `listen` para `3000`)
- laravel.conf.example -> plus.conf (altere o parametro `listen` para `8000`)

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

`docker push softv/nginx`

`docker push softv/php-fpm`

`docker push softv/workspace`

Obs.: Caso receba o erro "no route to host" verifique se não há nenhum container em execução com o comando `docker ps` e execute o comando `docker network prune` 

3 - Subir o serviço

`docker-compose up -d`

## Teste

Acesse as seguintes urls para confirmar:

`nginx:3000` -> GATEWAY

`nginx:8000` -> BANCO SANGUE

Checar se as portas foram expostas corretamento pelo Docker:

- Linux

`netstat -atunp | grep 3000`  
`netstat -atunp | grep 8000`

- Windows (CMD)

`netstat -n | find "3000"`  
`netstat -n | find "8000"`

## Erros

`ERR_EMPTY_RESPONDE`

Causa:  

Projeto não está sendo mapeado dentro dos containers.  

Solução:  

Em caso de troca de senha no Windows é necessário resetar as credenciais para que o projeto possa ser mapeado nos containers.

Clique com o botão direito no icone do docker --> Settings --> Shared Drivers --> Reset Credencials

Entre com a senha nova e reinicie os containers.

`Bind for 0.0.0.0:80: unexpected error Permission denied`

**Causa:**

A porta 80 do host já está em uso por outra aplicação.

**Solução:**
 
Abre o `.env` do sisa-docker e procure a seguinte configuração `NGINX_HTTP_PORT` e mude o valor para `88` ou outra porta que não estaja em uso. 