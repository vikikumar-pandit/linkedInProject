# Linkedin-Distributed — Social Media App (LinkedIn-style)

A distributed social networking backend built with Spring Boot microservices, modeling core LinkedIn-style domains: profiles, posts, and connections.

## What it does

Implements the core backend of a professional social network — user profiles, posting, a connections/network graph, and an activity feed — designed around microservice boundaries rather than a single monolith.

## Architecture

- **APIGateway** — single entry point routing requests to the appropriate downstream service
- **userService** — user profiles and account management
- **postsService** — post creation, storage, and retrieval
- **ConnectionsService** — manages the connections/network graph between users
- **uploader-service** — handles media/file uploads (e.g., profile pictures, post attachments)

Services communicate asynchronously via **Kafka** for feed generation (e.g., fanning out a new post to a user's network) and synchronously via **Feign clients** for direct inter-service calls, keeping services decoupled and independently deployable.

## Key features

- **Event-driven feed generation** — new posts and connection events are published to Kafka topics and consumed asynchronously, avoiding tight coupling and blocking calls between services.
- **Low-Level + High-Level Design focus** — each service's internal domain model (LLD) was designed deliberately, alongside the overall system architecture (HLD) for how services interact at scale.
- **Redis caching** — frequently accessed data (e.g., profile info, feed data) is cached to reduce database load and improve read performance.
- **Containerized deployment** — all services run in Docker containers, orchestrated with Kubernetes for fault tolerance and horizontal scalability.

## Tech stack

Java, Spring Boot, Spring Cloud Gateway, Kafka, Redis, Feign, Docker, Kubernetes

## Running locally

> Fill in your actual setup steps here, e.g.:
```bash
# Clone the repo
git clone https://github.com/vikikumar-pandit/linkedInProject.git
cd linkedInProject

# Start infra dependencies (Kafka, Redis, Postgres/Mongo) via docker-compose
docker-compose up -d

# Run each service
cd APIGateway && ./mvnw spring-boot:run
cd ../userService && ./mvnw spring-boot:run
cd ../postsService && ./mvnw spring-boot:run
cd ../ConnectionsService && ./mvnw spring-boot:run
```

## Status

Built as a personal project to practice distributed systems patterns — event-driven architecture, service decomposition, and caching strategies — in a realistic, LinkedIn-like domain.
