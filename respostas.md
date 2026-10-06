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
|3|EXPOSE |Faltava colocar a porta 80 no Dockerfile|A página funcionou, mas a porta não estava declarada no dockerfile|Adicionei EXPOSE 80|

6. Qual a diferença entre `-p 7042:80` e `-p 80:7042` no `docker run`? Qual dos dois números é a porta do container?



\-p 7042:80 = a porta 7042 é a porta do computador e a porta 80 é a porta do container. Quando acessar localhost:7042, a requisição é enviada para a porta 80 do container.



\-p 80:7042 = acontece ao contrário, a porta 80 é do PC que leva para a porta 7042 do container.



O formato é HOST:CONTAINER, que seria igual a explicação que passou na sala PRÉDIO:APARTAMENTO.





## Parte 4 · docker-compose.yml

7. No serviço `blog`, por que `WORDPRESS\\\\\\\_DB\\\\\\\_HOST` recebe `db` e não `localhost`?



Porque os containers se comunicam pelo docker compose usando o nome do serviço







8\. Por que o serviço `db` não publica a porta 3306? Se precisar consultar o banco, como faz sem publicar a porta? Mostre o comando.



Pois é o wordpress que precisa acessar o banco pela rede interna do Docker Compose, o que evita de expor o banco. Para consultar o banco poderia fazer:



docker compose exec db mariadb -u root -p







## Parte 5 · Persistência

9. Quais comandos você usou para derrubar e subir a stack? Qual comando teria apagado o post que você criou, e por quê?





Usei docker compose down para remover os containers e depois docker compose up -d para criar eles de novo. O comando que apagaria os dados seria:



docker compose down -v



pois o que usei ele só derrubou e não apagou o post 







10\. Código de conclusão impresso pelo verificador:

```
PS C:\\Users\\Aluno\\Downloads\\avaliacao-docker-agrovale> powershell -ExecutionPolicy Bypass -File scripts\\verificar.ps1

================================================================

&#x20;Verificador · Avaliação Prática de Docker · Turma A

================================================================

&#x20;Matrícula 26128006 · portal 8006 · blog 9006 · manutenção 7006



A. Arquivos, imagens e Git

\[ OK ] A1 portal/Dockerfile segue os requisitos

\[ OK ] A2 imagem manutencao:26128006 corrigida e servindo o aviso

\[ OK ] A3 .env fora do Git e .env.example versionado

\[ OK ] A4 5+ commits e remoto no GitHub (encontrados: 5)

\[ OK ] A5 imagem jeffsilva03/agrovale-portal:1.0-26128006 pública no Docker Hub



B. Stack em execução

\[ OK ] B1 serviços portal, blog e db em execução

\[ OK ] B2 portal roda a imagem publicada

\[ OK ] B3 portas: portal em 8006 e blog em 9006

\[ OK ] B4 db sem porta publicada e com volume nomeado

\[ OK ] B5 blog com volume nomeado em /var/www/html

\[ OK ] B6 rede própria compartilhada pelos três serviços

\[ OK ] B7 política de restart nos três serviços

\[ OK ] B8 nenhuma senha escrita direto no docker-compose.yml



C. Conteúdo e persistência

\[ OK ] C1 portal mostra seu nome e sua matrícula

\[ OK ] C2 WordPress instalado com a matrícula no título do site

\[ OK ] C3 post sobreviveu à recriação do blog (post 2026-10-06T00:28:11 · container 2026-10-06T00:33:15)



================================================================

&#x20;Resultado: 16/16 verificações

&#x20;Código de conclusão: AGROVALE-26128006-086AB452

&#x20;Copie o código para o respostas.md, faça o commit final e crie a tag v1.0.

================================================================
```

