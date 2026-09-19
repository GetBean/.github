# Bean 👋

**Bean is a friendship-first mobile app designed to help people discover events, join communities and build meaningful real-world connections.**

Making new friends as an adult can be difficult. Bean is being built to make that process feel more natural by helping people connect through shared interests, communities and events happening around them.

Bean is a full-stack production project spanning mobile development, backend engineering, web development and cloud infrastructure.

🌐 [getbean.io](https://getbean.io)

---

## About Bean

Bean is primarily a **mobile application** focused on friendship and real-world social connection.

The mobile experience is designed around helping people:

- 🎟️ Discover events
- 👥 Find and join groups and communities
- 🤝 Meet people with shared interests
- 💬 Communicate through real-time messaging
- 📍 Discover people and activities around them
- ❤️ Build meaningful friendships through shared experiences

Bean is currently under active development as a commercial product.

The production source repositories are private, but this GitHub organisation provides an overview of the applications, services, infrastructure and engineering behind the platform.

---

# Projects

Bean is made up of several independently developed applications and infrastructure projects.

## 📱 Bean-Mobile

**Bean-Mobile is the core Bean product and the primary application used by users.**

It is a cross-platform mobile application built with **React Native and Expo** for iOS and Android.

### Core Technologies

- React Native
- Expo
- Firebase Authentication
- Cloud Firestore
- Google Maps
- REST API integration
- TestFlight

### Responsibilities

The mobile application provides the main Bean experience, including areas such as:

- User registration and authentication
- User profiles
- Friendship and social discovery
- Events
- Groups and communities
- Real-time messaging
- Location-based discovery
- Media and profile content
- Social interactions

The application communicates with **Bean-API** for backend functionality while also integrating with services such as Firebase and Google Maps.

---

## ⚙️ Bean-API

**Bean-API is the backend service powering the Bean mobile application and supporting platforms.**

It is a production **Java 25 / Spring Boot REST API** responsible for Bean's core business logic, application data and integrations.

### Core Technologies

- Java 25
- Spring Boot
- Spring Security
- Spring Data JPA
- MySQL
- Firebase Authentication
- Firebase Admin SDK
- Cloud Firestore
- AWS S3
- Maven
- Bucket4j
- SonarCloud

### Responsibilities

Bean-API handles areas including:

- Authentication and authorisation
- User and profile management
- Events
- Groups and communities
- Social relationships
- Application business logic
- Media and file uploads
- Database persistence
- Firebase integrations
- AWS integrations
- Rate limiting
- Input validation
- API security
- Error handling

### Engineering Focus

The API is continuously reviewed and improved with a strong focus on:

- Authentication and authorisation
- BOLA / IDOR protection
- Firebase JWT validation
- API security
- Database consistency
- Upload and media security
- Rate limiting
- Resilience and error handling
- Logging and observability
- Automated testing
- Test coverage
- Dependency security
- Code quality
- Maintainability

---

## 🌐 Bean-Frontend

**Bean-Frontend is Bean's web application, separate from the mobile product.**

It supports Bean's public web presence as well as web-based management functionality.

The mobile application remains the primary consumer-facing Bean experience.

### Core Technologies

- Next.js
- React
- TypeScript
- Tailwind CSS

### Responsibilities

Bean-Frontend supports areas such as:

- Bean's public website
- Marketing pages
- Product information
- Web-based management functionality
- Internal and administrative interfaces
- Supporting experiences outside the mobile application

The frontend provides Bean with a modern web platform while allowing the mobile and web applications to evolve independently.

---

## ☁️ Bean-Infrastructure

**Bean-Infrastructure defines and manages the cloud infrastructure used to run Bean.**

The infrastructure has been designed around AWS managed services with a focus on security, maintainability, environment separation, scalability and sensible operating costs for an early-stage product.

### Core Technologies

- AWS
- Terraform
- ECS Fargate
- Docker
- Application Load Balancer
- Amazon RDS for MySQL
- Amazon S3
- Route 53
- CloudWatch
- Sentry

### Responsibilities

The infrastructure project covers areas including:

- Infrastructure as Code
- Development and production environments
- AWS networking
- Containerised application workloads
- API deployment
- Load balancing
- Database infrastructure
- DNS
- HTTPS routing
- Storage
- Secrets and configuration
- Logging
- Monitoring
- Observability

Bean-API runs as a containerised application on **Amazon ECS Fargate** behind an **Application Load Balancer**.

Application data is stored in a private **Amazon RDS for MySQL** database, with supporting AWS services used for storage, DNS, monitoring and application operations.

---

# Architecture

At a high level, Bean consists of four main projects:

```text
                        ┌─────────────────────────┐
                        │       Bean-Mobile       │
                        │                         │
                        │  React Native / Expo    │
                        │       iOS / Android     │
                        └────────────┬────────────┘
                                     │
                                     │ REST API
                                     ▼
                        ┌─────────────────────────┐
                        │        Bean-API         │
                        │                         │
                        │ Java 25 / Spring Boot   │
                        └────────────┬────────────┘
                                     │
                   ┌─────────────────┼─────────────────┐
                   │                 │                 │
                   ▼                 ▼                 ▼
              Amazon RDS          AWS S3           Firebase
                MySQL
                   │
                   │
                   ▼
            Application Data


        ┌─────────────────────────┐
        │      Bean-Frontend      │
        │                         │
        │ Next.js / React /       │
        │ TypeScript / Tailwind   │
        │                         │
        │ Marketing & Management  │
        └─────────────────────────┘


        ┌─────────────────────────┐
        │   Bean-Infrastructure   │
        │                         │
        │ AWS / Terraform / ECS   │
        │ RDS / S3 / Route 53     │
        └─────────────────────────┘
