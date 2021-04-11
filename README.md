# Curso Descomplicando Docker - LinuxTips

## Legenda Dockerfile:
```
ADD => Copia novos arquivos, diretórios, arquivos TAR ou arquivos remotos e os adicionam ao filesystem do container;

CMD => Executa um comando, diferente do RUN que executa o comando no momento em que está "buildando" a imagem, o CMD executa no início da execução do container;

LABEL => Adiciona metadados a imagem como versão, descrição e fabricante;

COPY => Copia novos arquivos e diretórios e os adicionam ao filesystem do container;

ENTRYPOINT => Permite você configurar um container para rodar um executável, e quando esse executável for finalizado, o container também será;

ENV => Informa variáveis de ambiente ao container;

EXPOSE => Informa qual porta o container estará ouvindo;

FROM => Indica qual imagem será utilizada como base, ela precisa ser a primeira linha do Dockerfile;

MAINTAINER => Autor da imagem; 

RUN => Executa qualquer comando em uma nova camada no topo da imagem e "commita" as alterações. Essas alterações você poderá utilizar nas próximas instruções de seu Dockerfile;

USER => Determina qual o usuário será utilizado na imagem. Por default é o root;

VOLUME => Permite a criação de um ponto de montagem no container;

WORKDIR => Responsável por mudar do diretório / (raiz) para o especificado nele;
```

## Comandos básicos DockerHub e Registry
```
docker image inspect debian
docker history linuxtips/apache:1.0
docker login
docker login registry.suaempresa.com
docker push linuxtips/apache:1.0
docker pull linuxtips/apache:1.0
docker image ls
docker container run -d -p 5000:5000 --restart=always --name registry registry:2
docker tag IMAGEMID localhost:5000/apache
```


## Legenda DockerMachine/Desktop
```
Para fazer a instalação do Docker Machine no Linux, faça:

curl -L https://github.com/docker/machine/releases/download/v0.16.1
/docker-machine-`uname -s`-`uname -m` >/tmp/docker-machine
chmod +x /tmp/docker-machine 
sudo cp /tmp/docker-machine /usr/local/bin/docker-machine


Para seguir com a instalação no macOS:

curl -L https://github.com/docker/machine/releases/download/v0.16.1
/docker-machine-`uname -s`-`uname -m` >/usr/local/bin/docker-machine 
chmod +x /usr/local/bin/docker-machine

Para seguir com a instalação no Windows caso esteja usando o Git bash:
if [[ ! -d "$HOME/bin" ]]; then mkdir -p "$HOME/bin"; fi
curl -L https://github.com/docker/machine/releases/download/v0.16.1
/docker-machine-Windows-x86_64.exe > "$HOME/bin/docker-machine.exe"
chmod +x "$HOME/bin/docker-machine.exe"


Para verificar se ele foi instalado e qual a sua versão, faça:

docker-machine version

docker-machine create --driver virtualbox linuxtips

docker-machine ls

docker-machine env linuxtips

eval "$(docker-machine env linuxtips)"

docker container ls

docker container run busybox echo "LINUXTIPS, VAIIII"

docker-machine ip linuxtips

docker-machine ssh linuxtips

docker-machine inspect linuxtips

docker-machine stop linuxtips

docker-machine ls 

docker-machine start linuxtips

docker-machine rm linuxtips

eval $(docker-machine env -u)
```

## Comandos básicos Docker Swarm
```
docker swarm init

docker swarm join --token \ SWMTKN-1-100_SEU_TOKEN SEU_IP_MASTER:2377

docker node ls

docker swarm join-token manager

docker swarm join-token worker

docker node inspect LINUXtips-02

docker node promote LINUXtips-03

docker node ls

docker node demote LINUXtips-03

docker swarm leave

docker swarm leave --force

docker node rm LINUXtips-03

docker service create --name webserver --replicas 5 -p 8080:80  nginx

curl QUALQUER_IP_NODES_CLUSTER:8080

docker service ls

docker service ps webserver

docker service inspect webserver

docker service logs -f webserver

docker service rm webserver

docker service create --name webserver --replicas 5 -p 8080:80 --mount type=volume,src=teste,dst=/app  nginx

docker network create -d overlay giropops

docker network ls

docker network inspect giropops

docker service scale giropops=5

docker network rm giropops

docker service create --name webserver --network giropops --replicas 5 -p 8080:80 --mount type=volume,src=teste,dst=/app  nginx

docker service update <OPCOES> <Nome_Service> 
```

## Secrets do swarm
```
echo 'minha secret' | docker secret create 
docker secret create minha_secret minha_secret.txt
docker secret inspect minha_secret
docker secret ls
docker secret rm minha_secret
docker service create --name app --detach=false --secret db_pass  minha_app:1.0
docker service create --detach=false --name app --secret source=db_pass,target=password,uid=2000,gid=3000,mode=0400 minha_app:1.0
ls -lhart /run/secrets/
docker service update --secret-rm db_pass --detach=false --secret-add source=db_pass_1,target=password app
```

## Docker-compose
```
docker stack deploy -c docker-compose.yml giropops
docker service ls 
docker stack ls

Prometheus:
http://SEU_IP:9090

AlertManager:
http://SEU_IP:9093

Grafana:
http://SEU_IP:3000

Node_Exporter:
http://SEU_IP:9100

Rocket.Chat:
http://SEU_IP:3080

cAdivisor:
http://SEU_IP:8080

docker stack rm giropops


Lembrando, para conhecer mais sobre o giropops-monitoring acesse o repositório no GitHub e assista a série de vídeos em que  falo detalhadamente como montei essa solução:
Repo: https://github.com/badtuxx/giropops-monitoring
Vídeos: https://www.youtube.com/playlist?list=PLf-O3X2-mxDls9uH8gyCQTnyXNMe10iml
```