# Linuxtips - Giropops Senhas

Para o projeto funcionar corretamente é necessário ter o redis rodando.

Você pode fazer isso com o seguinte comando
```bash
 docker container run -d --name redis-server -p 6379:6379 redis
```

Em seguida você deverá buildar essa imagem com o comando
```bash
 docker image build -t giropops-senha:1.0 .
```

Para rodar, utilize o seguinte comando
```bash
 docker container run -d --env REDIS_HOST=<REDIS_HOST> -p 5000:5000 --name giropops-senha giropops-senha:1.0
```
Se vc estiver rodando o redis através do container acima, você terá que ter o ip do container que está rodando para isso você poderá rodar
```bash
 docker container inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' redis-server
```

Uma opção para rodar tudo em um comando só seria:
```bash
 docker container run -d -e REDIS_HOST=$(docker container inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' redis-server) --name giropops-senhas -p 5000:5000 giropops-senhas
```
