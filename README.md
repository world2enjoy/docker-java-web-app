# java-web-app with docker

Below are the steps to run a java app by deploying into tomcat and the tomcat is running inside a docker container.

* clone the java code from this repository that contains the Dockerfile. Go to the repository directory.
* maven build: `mvn clean verify -DskipTests`
* build docker image: `sudo docker build -t my-app-image .`
* run the image as container: `sudo docker run --rm --name my-app-c -d -p 8081:8080 my-app-image`
* see the tomcat startup logs: `sudo docker logs my-app-c`
* curl to the localhost 8081: `curl http://localhost:8081/app/hello` . Above will send response from the servlet.
* get into the container: `sudo docker exec -it my-app-c bash`
* curl to the localhost of the container: `curl http://localhost:8080/app/hello`. Above will send response from the servlet.
