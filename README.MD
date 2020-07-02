### Docker API

`FROM node:current-slim`

###### FROM baseImage para e finir qual a imagem que será utilizada no projeto

###### No caso, current-slim é a versão enxuta mais atual do Node

`WORKDIR /usr/src/app`

###### WORKDIR representa o caminho dentro da imagem onde a aplicação ficará

`COPY package.json .`

###### COPY vai copiar um arquivo necessário para o funcionamento da aplicação,

###### nesse caso o package.json porque este possui as informações sobre as dependências

###### necessárias no projeto

###### O '.' no final do comando fala que o arquivo será copiado na RAÍZ do WORKDIR

`RUN npm install`

###### RUN roda um comando, nesse caso rodamos o npm install que vai instalar as dependências

###### do projeto

`EXPOSE 8080`

###### EXPOSE vai falar qual porta a aplicação estará acessível de dentro do nosso container

###### Mesmo nesse caso, onde a aplicação roda na porta 3000

`CMD ["npm", "start"]`

###### CMD executa uma lista de comandos no terminal, nesse caso é o comando de iniciar a aplicação

`COPY . .`

###### Copiamos de novo TUDO da aplicação para a raíz do container

###### Copiarei aqui alguns trechos do artigo:

Dentre os comandos que podemos executar, temos o docker image build, para criar uma imagem, e vamos utilizá-lo para gerar o que precisamos aqui.

Certifique-se que você está na raiz da API, a pasta docker-sample-api e execute o seguinte comando.

`docker image build -t dockerapi:1.0 .`

Para facilitar futuras execuções, vamos dar um nome para esta imagem, adicionando o parâmetro -t, seguido pelo nome:versão da imagem.

Por fim, devemos especificar o diretório onde está nosso Dockerfile, que no caso é a raiz da nossa API, definido no comando pelo ".".

A última coisa que precisamos fazer é pegar esta imagem gerada e executar ela como um contêiner, e isto é feito pelo comando docker container run.

Novamente, certifique-se que você está na raiz da API, a pasta docker-sample-api e execute o seguinte comando.

docker container run --publish 8080:3000 --detach --name api dockerapi:1.0
O primeiro parâmetro que temos no comando é o --publish, que vai fazer o redirecionamento do tráfego para a porta onde nossa API está rodando.

Neste caso, vamos rodar nosso contêiner na porta 8080, ou seja, acessaremos nossa API no Browser pela URL http://localhost:8080, porém, internamente nossa API está rodando na porta 3000.

O --publish cuidará exatamente deste redirecionamento de tráfego para nós. Você também pode alterar a porta de execução para outra qualquer, diferente da 8080 se quiser.

O --detach diz para o Docker executar este contêiner em background, e não vai travar o processo do nosso terminal ou Visual Studio Code que acabamos de executar.

O --name especifica o nome do contêiner, e fica a seu critério colocar qualquer nome que quiser, desde que não tenha espaços ou caracteres especiais.

Conteúdo retirado de um artigo do blog:
https://balta.io/blog/docker-instalacao-configuracao-e-primeiros-passos
