# Bean

**Bean is a friendship-first mobile app designed to help people find new friends, build genuine connections and develop meaningful real-world friendships.**

Making new friends as an adult can be difficult. Bean is being built to make that process easier and more natural by helping people discover others they genuinely connect with through shared interests, communities, activities and experiences.

At its core, Bean is about **helping people find their people**. Features such as messaging, groups, events and location-based discovery are designed to create more opportunities for friendships to start and grow.

Bean is a full-stack production project spanning **mobile development, backend engineering, web development, cloud infrastructure, CI/CD, security and observability**.

🌐 [getbean.io](https://getbean.io)

---

## About Bean

Bean is a **friendship-focused mobile application for iOS and Android** built around helping people meet, connect and form meaningful friendships.

The core experience is designed around helping people:

- 🤝 Find and connect with potential new friends
- ❤️ Meet people with shared interests and compatible lifestyles
- 💬 Turn new connections into conversations through real-time messaging
- 👥 Find and join groups and communities
- 📍 Discover people and social opportunities around them
- 🎟️ Use events and activities as opportunities to meet and connect in real life

Rather than treating events or communities as the end goal, Bean uses them as ways to make meeting people easier and give new friendships somewhere to begin.

Bean is currently under active development as a commercial product.

The production source repositories are private, but this GitHub organisation provides an overview of the applications, services, infrastructure and engineering behind the platform.

---

## Project Overview

Bean is made up of four primary projects:

| Project | Purpose | Key Technologies |
| --- | --- | --- |
| **Bean-Mobile** | Primary friendship-focused iOS and Android application | React Native, Expo, Firebase, Firestore, Google Maps |
| **Bean-Frontend** | Marketing website and web-based management application | Next.js, React, TypeScript, Tailwind CSS, AWS Amplify |
| **Bean-API** | Shared backend services, business logic and application data | Java 25, Spring Boot, MySQL, Firebase, AWS |
| **Bean-Infrastructure** | AWS infrastructure and application environments | Terraform, ECS Fargate, ECR, RDS, S3, CloudFront, Route 53 |

Both **Bean-Mobile** and **Bean-Frontend** can consume **Bean-API**, providing a shared backend for Bean's mobile, web-based management and supporting application experiences.

---

## 📱 Bean-Mobile

**Bean-Mobile is the core Bean product and the primary application used by users.**

It is a cross-platform mobile application built with **React Native and Expo** for iOS and Android, centred around helping people find new friends and turn those connections into real-world friendships.

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
- Finding people through shared interests
- Social connections and relationships
- Real-time messaging
- Groups and communities
- Event discovery
- Location-based discovery
- Media and profile content
- Social interactions

Bean-Mobile communicates with **Bean-API** for backend functionality while also integrating with services such as Firebase and Google Maps.

---

## 🌐 Bean-Frontend

**Bean-Frontend is Bean's web application, separate from the mobile product.**

It supports Bean's public web presence alongside web-based management and administrative functionality.

The **mobile application remains the primary consumer-facing Bean experience**, while Bean-Frontend provides supporting experiences for marketing, management and administration.

### Core Technologies

- Next.js
- React
- TypeScript
- Tailwind CSS
- AWS Amplify
- REST API integration

### Responsibilities

Bean-Frontend supports:

- Bean's public website
- Marketing pages
- Product information
- Web-based management functionality
- Internal and administrative interfaces
- Supporting experiences outside the mobile application
- Integration with Bean-API for application data and backend functionality

Bean-Frontend is hosted using **AWS Amplify** and communicates with **Bean-API** where backend functionality or application data is required.

The web application is developed independently from Bean-Mobile, allowing the mobile product and supporting web platform to evolve separately while sharing the same backend services where appropriate.

---

## ⚙️ Bean-API

**Bean-API is the shared backend service powering the Bean mobile application and supporting web platform.**

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
- Friendship and social relationships
- Social discovery
- Events
- Groups and communities
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

## ☁️ Bean-Infrastructure

**Bean-Infrastructure defines and manages the AWS infrastructure supporting Bean's backend platform.**

The infrastructure is managed using **Terraform** and maintains separate **Development and Production environments** built from reusable infrastructure modules.

The platform follows a public-edge/private-workload architecture, with application workloads and databases kept within private subnets while public traffic enters through managed edge services.

### Core Technologies

- AWS
- Terraform
- Amazon ECS Fargate
- Amazon ECR
- Application Load Balancer
- Amazon RDS for MySQL
- Amazon S3
- Amazon CloudFront
- Route 53
- AWS Certificate Manager
- AWS Secrets Manager
- AWS Systems Manager
- AWS IAM
- CloudWatch
- GitHub Actions
- OpenID Connect
- Docker

### Infrastructure Responsibilities

Bean-Infrastructure manages areas including:

- Development and production environment isolation
- VPC networking
- Public and private subnets
- Containerised ECS workloads
- Application load balancing
- Private MySQL database infrastructure
- ECR container repositories
- S3 media storage
- CloudFront media delivery
- DNS and TLS certificates
- Secrets management
- IAM roles and policies
- GitHub Actions OIDC integration
- Monitoring and alerting
- Remote Terraform state
- Administrative access to private infrastructure

Bean-API runs on **Amazon ECS Fargate** within private subnets and receives application traffic through an **Application Load Balancer**.

Application data is stored in a private **Amazon RDS for MySQL** database.

Media is stored in private **Amazon S3** buckets and delivered through **Amazon CloudFront**, allowing the underlying storage to remain non-public.

Administrative access to private infrastructure uses **AWS Systems Manager** rather than exposing SSH directly to the internet.

### Infrastructure Principles

The infrastructure is designed around:

- Infrastructure as Code
- Reusable Terraform modules
- Development and production isolation
- Remote and locked Terraform state
- Private application and database networking
- Least-privilege IAM
- Temporary AWS credentials
- Environment-specific secrets
- Environment-specific media storage
- Immutable container artifacts
- Build once, deploy many
- Explicit release promotion
- Explicit production deployment
- Artifact digest verification
- Reproducible infrastructure changes
- Cost-conscious AWS architecture

---

## 🔄 CI/CD

Bean uses **GitHub Actions** to automate continuous integration, container builds, development deployments, release promotion and production deployments for Bean-API.

The delivery model follows a **Build Once, Deploy Many** approach:

**Commit → Build → Staging → Development → Validation → Promotion → Release → Production**

Application artifacts are built once and stored as immutable container images in **Amazon ECR**. The same tested artifact is promoted through the release lifecycle rather than being rebuilt for production.

Release promotion and production deployment are intentionally separate operations, allowing an application version to be approved as a release without requiring it to be deployed immediately.

### Continuous Integration

Changes to Bean-API are validated through an automated pipeline covering:

- Unit tests
- Integration tests
- JaCoCo test coverage
- SonarQube static analysis and code quality
- Snyk dependency vulnerability scanning
- Docker image builds
- Amazon ECR publishing

Successful application builds produce versioned Docker images which are stored in a dedicated staging repository in **Amazon ECR**.

### Development Deployment

Successful builds from the main branch are automatically deployed to Bean's Development environment.

The deployment workflow:

1. Builds and validates the application
2. Creates a versioned Docker image
3. Publishes the image to Amazon ECR
4. Verifies that the selected image exists
5. Retrieves the current ECS task definition
6. Updates the task definition with the new image
7. Deploys the revision to Amazon ECS
8. Waits for the ECS service to reach a stable state

AWS access from GitHub Actions uses **OpenID Connect and IAM roles**, avoiding the need for long-lived AWS access keys within CI/CD.

### Release Promotion

Bean follows an artifact promotion approach for production releases.

A container image that has already been built and validated in Development can be promoted from the staging ECR repository into a dedicated release repository.

The promotion workflow:

1. Verifies that the selected staging image exists
2. Retrieves the tested image
3. Promotes it into the release repository
4. Verifies the resulting release artifact
5. Confirms that the staging and release image digests match

Digest verification ensures that the released artifact is the **same container image that was tested in Development**.

Promotion does not automatically deploy the image to Production.

### Production Deployment

Production deployments use previously promoted release images from Amazon ECR.

The production workflow:

1. Selects an existing released image
2. Verifies that the release exists
3. Retrieves the current Production ECS task definition
4. Renders a new task definition using the selected image
5. Registers the new task definition revision
6. Updates the Production ECS service
7. Waits for the deployment to stabilise

This keeps application build, release approval and production deployment as clearly separated stages.

---

## 🧪 Code Quality & Security

Quality and security checks are integrated into Bean's development lifecycle rather than being treated as separate activities.

### SonarQube

**SonarQube** is integrated into the Bean-API CI pipeline for static analysis and ongoing code quality monitoring.

Analysis runs alongside automated tests as part of continuous integration.

### JaCoCo

**JaCoCo** is used to generate Java test coverage reports during CI.

Test coverage is being expanded alongside Bean-API's automated unit and integration test suites.

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
- Private application networking
- Private database networking
- Role-based AWS access
- HTTPS at the public edge

---

## 📈 Monitoring & Observability

Bean uses monitoring, alerting and error tracking across both the application and cloud infrastructure.

### Sentry

**Sentry** provides application-level error tracking and diagnostics, helping identify runtime issues and understand failures within the application.

### Amazon CloudWatch

**Amazon CloudWatch** provides logging, metrics and infrastructure visibility across Bean's AWS environment.

Monitoring covers areas including:

- Application errors
- ECS workloads
- Load balancer health
- Database health
- Infrastructure behaviour
- Failed deployments
- Stopped ECS tasks
- Operational issues

Production infrastructure also uses automated alerting for key application and infrastructure conditions.

---

## 📖 Operations & Reliability

Bean includes supporting operational documentation alongside the application and infrastructure code.

Runbooks and architectural decision records are used to document procedures and trade-offs around areas such as:

- Production incident response
- Database recovery
- Deployment and rollback
- Infrastructure failures
- Secrets rotation
- Infrastructure hardening
- Architectural decisions and scaling trade-offs

This helps keep operational knowledge documented and makes infrastructure changes and incident response more repeatable.

---

## Architecture

At a high level, Bean consists of two independent client applications — the primary Bean mobile app and a supporting web application — both of which can consume a shared **Java / Spring Boot backend API**.

Bean-Mobile and Bean-Frontend sit at the same architectural level while serving different product purposes.

```text
     ┌───────────────────────────┐        ┌───────────────────────────┐
     │        Bean-Mobile        │        │       Bean-Frontend       │
     │                           │        │                           │
     │    React Native / Expo    │        │   Next.js / React /       │
     │       iOS / Android       │        │   TypeScript / Tailwind   │
     │                           │        │                           │
     │   Primary Bean Product    │        │ Marketing & Management    │
     └─────────────┬─────────────┘        └─────────────┬─────────────┘
                   │                                    │
                   │              REST API              │
                   └─────────────────┬──────────────────┘
                                     │
                                     ▼
                              Route 53 / HTTPS
                                     │
                                     ▼
                         Application Load Balancer
                                     │
                                     ▼
                        ┌─────────────────────────┐
                        │        Bean-API         │
                        │                         │
                        │ Java 25 / Spring Boot   │
                        │     ECS Fargate         │
                        │    Private Subnets      │
                        └────────────┬────────────┘
                                     │
                    ┌────────────────┼────────────────┐
                    │                │                │
                    ▼                ▼                ▼
               Amazon RDS         Amazon S3        Firebase
                 MySQL              Media
            Private Subnets           │
                                      ▼
                                  CloudFront
