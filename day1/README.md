# 🚀 Docker Basics and Microservices Deployment
 
 Welcome to my Docker Learning Repository! 👋  
 This repository documents my hands-on exploration of **Docker**, from understanding its core architecture to deploying **Spring Boot microservices**, managing **volumes**, **networks**, and even integrating **distributed tracing** with Zipkin.
 
 ---
 
 ## 📦 What I Did
 
 ### ✅ Core Concepts Covered
 
 - Traditional vs Containerized Deployment
 - Docker Architecture: Daemon, CLI, Images, Containers
 - Dockerfile & Image Building
 - Container Lifecycle Management
 - Volumes for Data Persistence
 - Docker Networking
 - Microservices Deployment with Docker
 - Tracing using Spring Cloud Sleuth + Zipkin
 
 ---
 
 ## 🐳 Docker Commands in Action
 
 ### ▶️ Running a Container
 
 ```bash
 # Running a REST API container
 docker run -p 5000:5000 muralisocial123/training/rest-api:1.0.0.RELEASE
 ```
 
 ### 🚀 Daemon Mode with Auto Restart
 
 ```bash
 docker run -p 5000:5000 -d --restart=always muralisocial123/training/rest-api:1.0.0.RELEASE
 ```
 
 ---
 
 ## 🔍 Container Management
 
 ```bash
 docker container ls             # Running containers
 docker container ls -a          # All containers
 docker container stop <id>      # Stop a container
 docker container start <id>     # Start a stopped container
 docker container prune          # Remove all stopped containers
 ```
 
 ---
 
 ## 📄 Dockerfile Example
 
 ```Dockerfile
 FROM openjdk:17
 MAINTAINER yourname@domain.com
 COPY target/app.jar app.jar
 EXPOSE 8080
 ENTRYPOINT ["java", "-jar", "app.jar"]
 ```
 
 Build your image:
 
 ```bash
 docker build -t yourname/app .
 ```
 
 ---
 
 ## 💾 Docker Volumes
 
 ```bash
 # Create a named volume
 docker volume create --name mydata
 
 # Mount it to a container
 docker run -it --rm -v mydata:/data ubuntu
 ```
 
 ---
 
 ## 🌐 Docker Networking
 
 ```bash
 # Create a custom bridge network
 docker network create mynetwork --subnet=10.0.0.0/16 --gateway=10.0.10.100
 
 # Run container in the custom network
 docker run -it --net mynetwork --name myubuntu ubuntu
 ```
 
 ---
 
 ## 🧹 Microservices Deployment
 
 - Built Spring Boot Microservices as Docker images using:
 
 ```bash
 mvn spring-boot:build-image -DskipTests
 ```
 
 - Used `docker-compose.yml` for orchestrating services
 
 ---
 
 ## 🔍 Distributed Tracing with Zipkin
 
 ```bash
 # Run Zipkin locally
 docker run -d -p 9411:9411 openzipkin/zipkin:2.23
 ```
 
 - Integrated Spring Cloud Sleuth with Zipkin to trace request flow across services.
 
 ---
 
 ## 📈 Monitoring and Logs
 
 ```bash
 docker logs -f <container_id>        # Tail logs
 docker stats                         # Real-time metrics
 docker top <container_id>            # Running processes in container
 ```
 
 ---
 
 ## 🙌 Final Thoughts
 
 This project gave me deep insights into real-world containerization, service isolation, persistent storage, and observability. Docker simplifies complex deployments, and I highly recommend exploring it if you're building scalable backend systems or microservices.
