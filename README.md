# PASSO A PASSO DE COMO INSTALAR  O DOCKER NO UBUNTU 16.04

## Introdução de Docker

<p align="justify">
O Docker é uma aplicação que torna simples e fácil executar processos de aplicação em um contêiner, que é como uma máquina virtual, apenas mais portátil, mais amigável, e mais dependente do sistema operacional do host.Para uma introdução detalhada aos diferentes componentes do contêiner Docker, confira The Docker Ecosystem: An Introduction to Common Components.Existem dois métodos para a instalação do Docker no Ubuntu 16.04. Um dos métodos envolve instalá-lo em uma instalação existente do sistema operacional.A outra envolve lançar um servidor com uma ferramenta chamada Docker Machine que instala o Docker automaticamente nele.
</p>

## Pré-requisitos

<p align="justify">
Para seguir esse tutorial, você vai precisar do seguinte: • Droplet do Ubuntu 16.04 64 bits• Usuário não-root com privilégios sudo (Initial Setup Guide for Ubuntu 16.04 explica como configurar isto).
Observação: O Docker requer uma versão de 64 bits do Ubuntu
Todos os comandos nesse tutorial devem ser executados como usuário não-root. Se o acesso de root for requerido para o comando, ele será precedido pelo sudo. Initial Setup Guide for Ubuntu 16.04 explica como adicionar usuários e dar a eles o acesso ao sudo.
</p>

## Instalando o Docker

<p align="justify">
O pacote de instalação do Docker disponível no repositório oficial do Ubuntu 16.04 pode não ser a última versão. Para obter a maior e mais recente versão, instale o Docker a partir do repositório oficial do Docker. Essa seção lhe mostra como fazer isso.
Mas primeiro, vamos atualizar o banco de dados de pacotes:
</p>

<pre>
$ sudo apt-get update
</pre>

Agora, vamos instalar o Docker. Adicione ao sistema a chave GPG oficial do repositório do Docker:

<pre>
 sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
 </pre>

Adicione o repositório do Docker às fontes do APT:

<pre>
$ sudo apt-add-repository 'deb https://apt.dockerproject.org/repo ubuntu-xenial main'
</pre>

Atualize o banco de dados de pacotes com os pacotes do Docker a partir do novo repositório adicionado:

<pre>
$ sudo apt-get update
</pre>

Certifique-se de que você está instalando a partir do repositório do Docker em vez do repositório padrão do Ubuntu 16.04:

<pre>
$ apt-cache policy docker-engine
</pre>

Você deverá ver uma saída semelhante à seguinte:

<pre>
Output of apt-cache policy docker-enginedocker-engine: Installed: (none)  Candidate: 1.11.1-0~xenial  Version table:     1.11.1-0~xenial 500        500 https://apt.dockerproject.org/repo ubuntu-xenial/main amd64 Packages     1.11.0-0~xenial 500        500 https://apt.dockerproject.org/repo ubuntu-xenial/main amd64 Packages
</pre>

Observe que o docker-engine não está instalado, mas o candidato para instalação é do repositório Docker do Ubuntu 16.04. O número da versão do docker-engine pode ser diferente.
Finalmente, instale o Docker:

<pre>
$ sudo apt-get install -y docker-engine
</pre>

O Docker agora será instalado, o daemon iniciado, e o processo habilitado para iniciar no boot. Verifique que ele está executando:

<pre>
$ sudo systemctl status docker
</pre>

A saída deve ser similar ao seguinte, mostrando que o serviço está ativo e em execução:<pre>[ secondary_label Output]● docker.service - Docker Application Container Engine   Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)   Active: active (running) since Sun 2016-05-01 06:53:52 CDT; 1 weeks 3 days ago     Docs: https://docs.docker.com Main PID: 749 (docker)</pre>

# Docker com Apache

Imagem docker criada para servir como base de estudos ao servidor web apache.

## Uso

<Strong> Utilize:</Strong>

<pre>docker run -dit --name apache-app --publish=9081:80 chicocx/docker-apache</pre>

<Strong>Para configurar externamente à imagem docker o local onde o apache salvará o site, utilize:</Strong>

<pre>docker run -dit --name apache-app --publish=9081:80 -v "$PWD":/usr/local/apache2/htdocs/ chicocx/docker-apache</pre>

<Strong>O parâmetro </Strong> <pre>-v "$PWD":/usr/local/apache2/htdocs/</pre>configura o diretório de onde o comando docker é executado como sendo o ponto de montagem do diretório /usr/local/apache2/htdocs/ da imagem criada. No caso, "$PWD" retorna o diretório atual.

<Strong>É possível modificar esse diretório da seguinte forma:</Strong>

<pre>-v /diretorio/do/host:/usr/local/apache2/htdocs/</pre>

Dessa forma, /diretorio/do/host passa a ser o diretório do host que conterá os arquivos lidos pela imagem em /usr/local/apache2/htdocs/

# Demais comandos

<Strong> Entrar na máquina/imagem</Strong>

<pre>
docker exec -it redmine1 bash
</pre>

<Strong>Sair sem encerrar a máquina: </Strong>

<pre>ctrl p q</pre>

<Strong> Lista o status dos containers </Strong>

<pre>docker ps -a</pre>

<Strong> Exclui os containers que estão parados</Strong>

<pre>
docker rm $(docker ps -q -f status=exited)
</pre>

<Strong>Lista as imagens baixadas</Strong>
<pre>
docker images
</pre>

<Strong> Exclui alguma imagem</Strong>
<pre>
docker rmi f72216345d97
</pre>
