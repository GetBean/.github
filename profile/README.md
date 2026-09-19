# Bean

**Bean is a friendship-first mobile app designed to help people discover events, join communities and build meaningful real-world connections.**

Making new friends as an adult can be difficult. Bean is being built to make that process feel more natural by helping people connect through shared interests, communities and events happening around them.

Bean is a full-stack production project spanning **mobile development, backend engineering, web development, cloud infrastructure, CI/CD, security and observability**.

🌐 [getbean.io](https://getbean.io)

---

## About Bean

Bean is primarily a **mobile application for iOS and Android**, focused on friendship and real-world social connection.

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

## Project Overview

Bean is made up of four primary projects:

| Project | Purpose | Key Technologies |
| --- | --- | --- |
| **Bean-Mobile** | Primary iOS and Android mobile application | React Native, Expo, Firebase, Firestore |
| **Bean-API** | Backend services, business logic and application data | Java 25, Spring Boot, MySQL, Firebase, AWS |
| **Bean-Frontend** | Marketing website and web-based management application | Next.js, React, TypeScript, Tailwind CSS |
| **Bean-Infrastructure** | Cloud infrastructure, environments and application delivery | AWS, Terraform, ECS Fargate, ECR, RDS, S3, GitHub Actions |

---

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

The mobile application provides the main Bean experience, including:

- User registration and authentication
- User profiles
- Friendship and social discovery
- Event discovery
- Groups and communities
- Real-time messaging
- Location-based discovery
- Media and profile content
- Social interactions

Bean-Mobile communicates with **Bean-API** for backend functionality while also integrating with services such as Firebase and Google Maps.

---

## ⚙️ Bean-API

**Bean-API is the backend service powering the Bean mobile application and supporting platforms.**

It is a production **Java 25 / Spring Boot REST API** responsible for Bean's core business logic, application data, security and external integrations.

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
- SonarQube
- JaCoCo
- Snyk
- Sentry

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

The API is continuously reviewed and improved with a focus on **security, reliability, testability and maintainability**.

Current areas of engineering work include:

- Authentication and authorisation
- BOLA / IDOR protection
- Firebase JWT validation
- API security
- Database consistency
- Secure media and file handling
- Rate limiting
- Resilience and error handling
- Logging and observability
- Automated unit and integration testing
- Test coverage
- Dependency security
- Static analysis
- Code quality and maintainability

---

## 🌐 Bean-Frontend

**Bean-Frontend is Bean's web application, separate from the mobile product.**

It supports Bean's public web presence as well as web-based management and administrative functionality.

The **mobile application remains the primary consumer-facing Bean experience**.

### Core Technologies

- Next.js
- React
- TypeScript
- Tailwind CSS

### Responsibilities

Bean-Frontend supports:

- Bean's public website
- Marketing pages
- Product information
- Web-based management functionality
- Internal and administrative interfaces
- Supporting experiences outside the mobile application

The web application is developed independently from Bean-Mobile, allowing the mobile product and supporting web platform to evolve separately.

---

## ☁️ Bean-Infrastructure

**Bean-Infrastructure defines and manages the cloud infrastructure used to run Bean.**

Bean's infrastructure is built on AWS and managed using **Terraform**, with a focus on security, maintainability, environment separation, scalability and sensible operating costs for an early-stage product.

### Core Technologies

- AWS
- Terraform
- GitHub Actions
- Amazon ECS Fargate
- Amazon ECR
- Docker
- Application Load Balancer
- Amazon RDS for MySQL
- Amazon S3
- Route 53
- CloudWatch
- Sentry

### Responsibilities

Bean-Infrastructure covers:

- Infrastructure as Code
- Development and production environments
- AWS networking
- Containerised application workloads
- API deployment
- Container image management
- Load balancing
- Database infrastructure
- DNS and HTTPS routing
- Object storage
- Secrets and configuration
- Logging
- Monitoring
- Observability
- CI/CD integration

Bean-API runs as a containerised application on **Amazon ECS Fargate** behind an **Application Load Balancer**.

Application data is stored in a private **Amazon RDS for MySQL** database, with supporting AWS services providing storage, DNS, monitoring and application operations.

---

## 🔄 CI/CD

Bean uses **GitHub Actions** to automate continuous integration, container builds, development deployments, release promotion and production deployments.

The delivery process is designed to keep application builds reproducible and to promote tested container images through the deployment lifecycle rather than rebuilding them for each environment.

### Continuous Integration

Changes to Bean-API are validated through an automated pipeline covering:

- Unit tests
- Integration tests
- JaCoCo test coverage
- SonarQube static analysis
- Snyk dependency vulnerability scanning
- Docker image builds
- Amazon ECR publishing

Successful application builds produce versioned Docker images which are stored in **Amazon ECR**.

### Development Deployment

Successful builds from the main branch are automatically deployed to Bean's development environment.

The deployment workflow:

1. Builds and validates the application
2. Creates a versioned Docker image
3. Publishes the image to Amazon ECR
4. Retrieves the current ECS task definition
5. Updates the task definition with the new image
6. Deploys the revision to Amazon ECS
7. Waits for the ECS service to reach a stable state

AWS access from GitHub Actions uses **OIDC and IAM roles**, avoiding the need for long-lived AWS access keys within CI/CD.

### Release Promotion

Bean follows an artifact promotion approach for production releases.

Tested container images are promoted from a staging ECR repository into a dedicated release repository.

The promotion workflow verifies image digests to ensure that the release artifact is identical to the tested artifact.

This allows the same immutable application image to progress through the release lifecycle rather than rebuilding the application for production.

### Production Deployment

Production deployments use previously promoted release images from Amazon ECR.

The production workflow verifies that the requested release exists, retrieves its image digest, updates the ECS task definition and deploys the release to the production ECS service.

This provides a controlled separation between:

**Build → Development → Release Promotion → Production**

---

## 🧪 Code Quality & Security

Quality and security checks are integrated into Bean's development lifecycle rather than being treated as separate activities.

### SonarQube

**SonarQube** is integrated into the Bean-API CI pipeline for static analysis and ongoing code quality monitoring.

Analysis is run alongside automated tests as part of continuous integration.

### JaCoCo

**JaCoCo** is used to generate Java test coverage reports during CI.

Test coverage is being expanded alongside the API's automated unit and integration test suites.

### Snyk

**Snyk** is integrated into the CI pipeline to identify known vulnerabilities in project dependencies.

### Application Security

Security work across Bean includes areas such as:

- Authentication and authorisation
- Firebase JWT validation
- BOLA / IDOR protection
- Dependency vulnerability management
- Input validation
- Secure file and media handling
- Rate limiting
- AWS IAM permissions
- Environment and secret separation

---

## 📈 Monitoring & Observability

Bean uses monitoring and error tracking across both the application and cloud infrastructure.

### Sentry

**Sentry** provides application-level error tracking and diagnostics, helping identify runtime issues and understand failures within the application.

### Amazon CloudWatch

**Amazon CloudWatch** is used for AWS logging and infrastructure monitoring across Bean's backend environment.

Together, these provide visibility across:

- Application errors
- Runtime behaviour
- Container workloads
- Infrastructure
- Deployments
- Operational issues

---

## Architecture

At a high level, Bean consists of a mobile application, supporting web application, backend API and the cloud infrastructure used to operate the platform.

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
               ┌─────────────────┼──────────────────┐
               │                 │                  │
               ▼                 ▼                  ▼
          Amazon RDS          Amazon S3          Firebase
            MySQL
               │
               ▼
        Application Data


        ┌──────────────────────────────┐
        │        Bean-Frontend         │
        │                              │
        │ Next.js / React / TypeScript │
        │                              │
        │   Marketing & Management     │
        └──────────────────────────────┘
