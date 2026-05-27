# Hoàng Ngọc Linh

Ho Chi Minh, Vietnam | +84 344 965 661 | linhhn.bkdn@gmail.com  
LinkedIn: [linkedin.com/in/li-hnl](https://www.linkedin.com/in/li-hnl/) | GitHub: [github.com/linhhnbkdn](https://github.com/linhhnbkdn)

---

## PROFESSIONAL SUMMARY
Principal Software Engineer with **8+ years** designing and scaling backend systems on AWS and Kubernetes — from a mechatronics background turned deep software engineering. Currently leading platform and AI engineering at Money Forward Vietnam: architected an internal **AI Agent platform** (LangChain, RAG, Function Calling, FastAPI) and scaled invoice-processing services to **10k concurrent users / 3k transactions per day** with KEDA-driven autoscaling on EKS. Strengths: pragmatic architecture, mentorship, and shipping production systems with measurable impact.

---

## EDUCATION
**Da Nang University of Science and Technology**  
*Bachelor's Degree in Mechatronics Engineering*  
**Duration**: Aug 2013 – Aug 2018 | GPA: 3.16/4

---

## CERTIFICATIONS
- **Professional Scrum Master™ I (PSM I)**
- **AWS Certified Solutions Architect – Professional**
- **AWS Certified Solutions Architect – Associate**
- **AWS Certified Cloud Practitioner**
- **Certificate AI Practitioner** — VTC Academy
- **Certificate CNN in TensorFlow** — deeplearning.ai
- **Certificate AI for Everyone** — deeplearning.ai

---

## AWARDS
- **MVP — Most Valuable Performer Award, Q1/2025**
- **MVP — Most Valuable Performer Award, 2023**
- **MVT — Most Valuable Team Award, 2023**: Recognized for exceptional technical delivery and cross-functional collaboration.

---

## SKILLS
- **Languages**: Python (5+ years), Go, Terraform
- **Backend Frameworks**: Django, DRF (5+ years), Celery (5+ years), FastAPI (3+ years), Flask, Gin
- **Frontend**: ReactJS, TypeScript, JavaScript, Tailwind CSS
- **Cloud & Infrastructure**: AWS (EKS, SQS, S3, SNS, RDS, Cognito, KMS), Docker, Kubernetes, KEDA
- **Data & Messaging**: PostgreSQL, MySQL, Redis, Kafka, ELK, PySpark, Apache Airflow
- **AI / ML**: Generative AI (LangChain, RAG, Function Calling, Llama), Computer Vision (SVM, VGG16), TensorFlow
- **Architecture & Practices**: Microservices, Clean Architecture, DDD, SOLID, Design Patterns, TDD, Agile/Scrum, CI/CD (CircleCI)
- **Authentication & Security**: JWT, OAuth2

---

## PROFESSIONAL EXPERIENCE

### **MONEY FORWARD VIETNAM**  
*Principal Software Engineer (formerly Technical Lead)* — **Jan 2022 – Present**  
A fintech company headquartered in Japan.  
**Responsibilities**:
- Architected and operated production microservices on EKS serving **10k+ concurrent users** in fintech workloads.
- Owned platform reliability — monitoring, capacity planning, and incident response across AWS and Kubernetes.
- Established repository structure, coding standards, and design-pattern guidelines for a 10-engineer team.
- Built and operated CI/CD pipelines (CircleCI) spanning development, staging, and production.
- Mentored engineers on backend, cloud, and AI/ML stacks; led code reviews to raise team-wide quality.
- Led Agile ceremonies — sprint planning, retrospectives, and daily stand-ups.
- Partnered with Product Managers and Owners to translate business requirements into technical solutions.

### **PARCEL PERFORM TECH HUB VIETNAM**  
*Backend Engineer* — **Sep 2021 – Jan 2022**  
Provider of end-to-end data and delivery-experience platforms for e-commerce businesses.  
**Responsibilities**:
- Built authentication and notification microservices (JWT, OAuth2) for a parcel-tracking platform processing **~1 million writes/day**.
- Designed async task pipelines on Kafka (message broker) and Celery (workers) to absorb spiky logistics traffic.
- Tuned services for availability and performance in close collaboration with the platform team.

### **AMPERE COMPUTING VIETNAM**  
*Backend Engineer* — **Mar 2019 – Sep 2021**  
An American fabless semiconductor company developing processors for large-scale server environments.  
**Responsibilities**:
- Built backend services for hardware-test automation and log analytics, accelerating QA regression cycles.
- Trained SVM classifiers for object-classification tasks in the chip-validation pipeline.
- Optimized backend systems and contributed to code reviews, bug fixing, and feature enhancements.

### **QUANG TRUNG SOFTWARE CITY**  
*Full-stack Engineer* — **Jan 2016 – Mar 2019**  
Software company specializing in product development and emerging-technology research for global clients.  
**Responsibilities**:
- Shipped end-to-end IoT prototypes — Arduino firmware, Django backend, web dashboard — demoed directly to clients.
- Researched and prototyped emerging IoT stacks for client-facing R&D projects.

---

## KEY PROJECTS

### **AI Agent Platform** (Jan 2025 – Present)  
**Customer**: Money Forward Vietnam  
**Description**: Internal Generative-AI platform providing a shared protocol and plug-and-play deployment for production AI Agents — supports **RAG** over enterprise data, structured **Function Calling**, and async task orchestration. Powers AI features across the Money Forward Vietnam product surface.  
- **Team Size**: 10  
- **My Position**: Principal Software Engineer  
**Responsibilities**:
- Designed the protocol and core abstractions for plug-and-play AI Agent deployment.
- Built AI runtime services with **FastAPI, LangChain, Celery, and Pydantic**, deployed on EKS via Terraform.
- Integrated AWS KMS for secure handling of model credentials and customer data.
- Implemented autoscaling with KEDA, SQS, and pod CPU/memory triggers.
- Led architecture design — DDD documentation, UML diagrams, and team-wide RFCs.
- Conducted code reviews, performance optimizations, and Agile cadence.

**Technologies**: LangChain, RAG, Function Calling, FastAPI, Pydantic, Celery, Gin; EKS, SQS, S3, SNS, Sendgrid, Cognito, Redis, AWS KMS.

### **Cloud Invoice Platform** (Jan 2022 – Present)  
**Customer**: Money Forward Vietnam  
**Description**: Two-product cloud platform — **invoice receiving** (OCR, reconciliation, payment processing) and **invoice sending** (compose, deliver, track) — built on event-driven microservices with KEDA-driven autoscaling.  
- **Scale**: Receiving — 10k concurrent users, 3k transactions/day. Sending — 5k concurrent users, 2k transactions/day.  
- **Team Size**: 10  
- **My Position**: Principal Software Engineer  
**Responsibilities**:
- Designed AWS infrastructure on EKS provisioned with Terraform.
- Scaled processing with KEDA-driven autoscaling (SQS depth + pod CPU/memory triggers).
- Authored Dockerfiles and Docker Compose stacks for dev/staging/production parity.
- Led application design — DDD documentation and UML diagrams.
- Developed GraphQL APIs (Graphene-Django) alongside REST (DRF) and async services (Celery).
- Conducted code reviews, optimizations, and bug fixing.

**Technologies**: Microservices; Django, DRF, Graphene-Django, Celery, Gin; EKS, SQS, S3, SNS, Sendgrid, Cognito, Redis.

### **PP Core System** (Sep 2021 – Jan 2022)  
**Customer**: Parcel Perform Tech Hub Vietnam  
**Description**: Core logistics platform for parcel tracking, notifications, and distance/route optimization.  
- **Writes per day**: ~1 million  
- **Team Size**: 12  
- **My Position**: Backend Engineer  
**Responsibilities**:
- Designed and built authentication, authorization, and notification microservices.
- Implemented JWT-based authentication and OAuth2 flows.
- Built async pipelines with Kafka (message broker) and Celery (workers).
- Developed internal authentication APIs with FastAPI.

**Technologies**: Microservices; Docker Compose; Django, Celery, DRF, FastAPI; Kafka.

### **Avion** (Mar 2019 – Sep 2021)  
**Customer**: Ampere Computing Vietnam  
**Description**: Internal application for executing hardware test cases, storing logs, and providing search and statistics for chip validation.  
- **Team Size**: 5  
- **My Position**: Backend Engineer  
**Responsibilities**:
- Designed monolithic MVC architecture for test orchestration.
- Built templating layer in HTML and JavaScript.
- Implemented session-based authentication and Flask internal APIs.

**Technologies**: Django, Flask, Celery, DRF; Docker Compose.

### **IoT Ampere** (Jan 2016 – Mar 2019)  
**Customer**: Quang Trung Software City  
**Description**: Arduino-based real-time current-monitoring system — sensor data is transmitted to a Django web dashboard for fast, accurate online visualization.  
- **Team Size**: 5  
- **My Position**: Full-stack Engineer  
**Responsibilities**:
- Designed end-to-end IoT pipeline — Arduino firmware → backend ingestion → web visualization.
- Programmed Arduino device firmware (Arduino IDE).
- Built backend APIs with Django and templating layer in HTML/JavaScript.

**Technologies**: Django, Celery, DRF; Docker Compose; Arduino device.

---

## LANGUAGES
- **Vietnamese**: Native  
- **English**: Professional working proficiency

---

## ADDITIONAL INFORMATION
- Extensive experience with **microservices architecture** and cloud-native applications on **AWS**.
- Production exposure to **Generative AI** (LangChain, RAG, Function Calling) through the AI Agent Platform at Money Forward Vietnam.
- Skilled in **CI/CD**, **Docker**, **Kubernetes**, **PySpark**, **Apache Airflow**, and **Computer Vision**.
- Passionate about applying machine learning and AI in production systems with measurable business impact.
