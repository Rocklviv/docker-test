# docker-test
Multilevel with docker.
###### Build project
Go to tomcat and build: <br>
```language-bash
docker build --no-cache -t rock/tomcat
```

Go to JavaApp and build: <br>
```language-bash
docker build -t rock/sampleapp
```

And run: <br>
```language-bash
docker run -t -i rock/sampleapp
```
