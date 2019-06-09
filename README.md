# vagrant-docker-project
Trabalho prático da disciplina de Tópicos Avançados em Redes de Computadores e Sistemas Distribuidos. UFScar Sorocaba

CONFIGURAÇÃO

1-No diretório do Vagrantfile digitar o comando:
$ vagrant up

2-Acessar antes a VM Master para pegar o token para poder adicionar worker com o comando abaixo (Descobrir como fazer isso direto pelo Vagrantfile):
$ vagrant ssh vmmaster
$ sudo docker swarm join-token worker

Copiar o comando que apareceu, acessar VM Worker:
$ vagrant ssh vmworker

Colar o comando com pre-fixo sudo.

4-Entrar novamente na VM Master e digitar o comando abaixo
sudo docker service create --name webservice1 --network ClusterNet --replicas 2 -p 5000:80 renatoar/docker-example

