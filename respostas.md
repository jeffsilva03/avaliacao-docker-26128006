# Respostas · Avaliação Prática de Docker · Cooperativa AgroVale (Turma A)

Nome: Jefferson Silva

Matrícula: 26128006

Usuário do GitHub: jeffsilva03

Usuário do Docker Hub: jeffsilva03

Responda com as suas palavras e com o que aconteceu na SUA máquina. Resposta curta e certa vale mais
do que texto longo copiado. Resposta que contradiz o seu próprio Dockerfile ou compose vale zero.

## Parte 1 · Dockerfile do portal

1. Qual imagem base você usou e qual o tamanho final da imagem do portal (saída de `docker images`)?



A imagem que usei foi a  nginx:1.27-alpine, conforme solicitado no PDF. Na saída do docker images, a imagem do portal ficou com 73.6 MB.



2\. Em qual pasta do container o Nginx procura os arquivos do site? Mostre o comando que você usou para
conferir que o `index.html` está lá dentro.



O Nginx busca os arquivos do site em /usr/share/nginx/html/ e pra conferir o index.html dentro do container, usei o comando :docker exec teste-portal ls -l /usr/share/nginx/html/index.html





## Parte 2 · Docker Hub

3. Nome completo da imagem publicada e link público do repositório no Docker Hub.



jeffsilva03/agrovale-portal:1.0-26128006.



4\. Por que o `docker login` foi feito com um token de acesso e não com a senha da conta?

Pois o token de acesso é mais seguro do que utilizar diretamente a senha da conta, caso tenha algum problema o token expira e não é necessário trocar a senha da conta toda



## Parte 3 · Página de manutenção

5. Preencha uma linha por defeito encontrado. Defeito inexistente listado aqui desconta pontos.

|#|Instrução|O que estava errado|O que você viu acontecer|Como corrigiu|
|-|-|-|-|-|
|1|COPY|O DockerFile não puxava o index.html para a imagem, então aparecia a página padrão do NGINX|O container rodou mas apareceu a mensagem do nginx|Adicionei o COPY para copiar a página de manutenção|
|2|WORKDIR|Estava levando para /usr/share/nginx em vez da pasta correta|Mesmo com o arquivo copiado, continuou aparecendo a mensagem do nginx|Troquei para /usr/share/nginx/html|
|3|||||

6. Qual a diferença entre `-p 7042:80` e `-p 80:7042` no `docker run`? Qual dos dois números é a porta do container?



\-p 7042:80 = a porta 7042 é a porta do computador e a porta 80 é a porta do container. Quando acessar localhost:7042, a requisição é enviada para a porta 80 do container.



\-p 80:7042 = acontece ao contrário, a porta 80 é do PC que leva para a porta 7042 do container.



O formato é HOST:CONTAINER, que seria igual a explicação que passou na sala PRÉDIO:APARTAMENTO.





## Parte 4 · docker-compose.yml

7. No serviço `blog`, por que `WORDPRESS\\\\\\\_DB\\\\\\\_HOST` recebe `db` e não `localhost`?
8. Por que o serviço `db` não publica a porta 3306? Se precisar consultar o banco, como faz sem publicar
a porta? Mostre o comando.

## Parte 5 · Persistência

9. Quais comandos você usou para derrubar e subir a stack? Qual comando teria apagado o post que você criou,
e por quê?
10. Código de conclusão impresso pelo verificador:

```
(cole aqui)
```

