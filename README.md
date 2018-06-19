

SERVER
ssh ubuntu@34.219.148.25

01
ssh ubuntu@18.237.240.175

02
ssh ubuntu@18.236.228.155





INSTALAR RANCHER
$ docker run -d --name rancher --restart=unless-stopped -p 8080:8080 -p 443:443 rancher/server:v1.6.18



DNS

	*.fraudfinder.com.br


Docker 17.03-ce
$ curl https://releases.rancher.com/install-docker/17.03.sh | sh

Docker Remover
$ sudo apt-get remove docker docker-engine docker.io


$ Deploy do traefik - DNS
# kubectl apply -f deployment.yml
