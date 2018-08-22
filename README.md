# java-web-app with docker
mvn clean verify -DskipTest <br/>
sudo docker build -t appi . <br/>
sudo docker run --name=webapp -d -p 8081:8080 appi<br/>
curl http://localhost:8081/app/hello?url=test<br/>
