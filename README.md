# TaskSphere: Scalable Task Management System

## **Overview**
The **TaskSphere** project is a scalable, cloud-native Task Management System designed for efficient task creation, assignment, and tracking. It ensures real-time collaboration for teams, leveraging modern backend technologies, robust messaging systems, and advanced monitoring tools. This production-ready application adheres to enterprise-grade standards and best practices.

---

## **Tech Stack Overview**
- **Backend**: Spring Boot (modular microservices and APIs).  
- **Message Broker**: Apache Kafka (real-time messaging).  
- **Containerization**: Docker for packaging applications.  
- **Orchestration**: Kubernetes (AKS) for managing containers in the cloud.  
- **API Documentation**: Swagger for API testing and documentation.  
- **Database**: MongoDB (via Azure Cosmos DB with Mongo API).  
- **CI/CD**: Jenkins for automated pipelines.  
- **Monitoring**: Spring Boot Actuator and Elasticsearch for metrics and logs.  
- **Testing**: JUnit for comprehensive testing.  
- **Version Control**: Git (GitHub repository).  
- **Project Management**: Jira for team collaboration.  
- **Authentication**: Keycloak (self-hosted) or Azure AD (alternative).  
- **Cloud**: Azure Free Tier (Azure Kubernetes Service and Cosmos DB).

---

## **Key Features**
### **1. User Authentication and Authorization**
- Centralized authentication using Keycloak.  
- Role-based access control for Admin, Manager, and Member roles.

### **2. Task Management**
- CRUD operations for tasks.  
- Task assignment and prioritization (High, Medium, Low).  
- Tracking task statuses: Pending, In Progress, Completed.

### **3. Real-Time Notifications**
- Apache Kafka for event-driven notifications.  
- Decoupled microservices for scalability.

### **4. Search and Analytics**
- Elasticsearch for advanced task search and analytics.  
- Productivity insights and completion trends.

### **5. API Documentation and Testing**
- Swagger UI for API testing and documentation.  
- Comprehensive unit and integration tests with JUnit.

### **6. CI/CD Pipeline**
- Jenkins pipeline automates build, test, and deployment stages.  
- Azure Kubernetes Service (AKS) deployment.

### **7. Monitoring and Logging**
- Spring Boot Actuator for performance metrics and health checks.  
- Elasticsearch for log aggregation and analysis.

### **8. Cloud-Native Deployment**
- Hosted on Azure Free Tier.  
- Scalable infrastructure using AKS and Cosmos DB.

---

## **System Architecture**
### **1. Microservices**
- **Auth Service**: Manages user login, registration, and roles.  
- **Task Service**: Handles task-related CRUD operations and updates.  
- **Notification Service**: Consumes Kafka events for real-time notifications.  
- **Analytics Service**: Analyzes team productivity and task progress.

### **2. Data Flow**
- User actions trigger Kafka events.  
- Services communicate via REST APIs and Kafka.

### **3. Storage**
- MongoDB for storing structured task and user data.

---

## **Setup Instructions**

### **1. Clone Repository**
```bash
git clone <repository-url>
cd TaskSphere
```

### **2. Prerequisites**
- **Java**: JDK 17+  
- **Docker**: Installed and running  
- **Kubernetes CLI**: Install `kubectl`  
- **Azure CLI**: Configure your Azure account  
- **Kafka**: Setup locally or use a managed service  
- **MongoDB**: Local instance or Azure Cosmos DB  
- **Keycloak**: Install and configure locally  

### **3. Environment Variables**
Create a `.env` file to configure sensitive data:
```env
SPRING_DATASOURCE_URL=<MongoDB_URL>
KAFKA_BOOTSTRAP_SERVERS=<Kafka_Server>
KEYCLOAK_URL=<Keycloak_URL>
AZURE_STORAGE_CONNECTION=<Azure_Cosmos_DB_Connection_String>
```

---

## **Running Locally**
1. **Start Kafka Broker**:  
   Use the Kafka binaries or Docker image.  
   ```bash
   docker-compose -f kafka-docker-compose.yml up
   ```
   
2. **Start MongoDB**:
   ```bash
   docker run -d -p 27017:27017 mongo
   ```
   
3. **Run Microservices**:
   Navigate to each microservice folder and start the Spring Boot application:
   ```bash
   ./mvnw spring-boot:run
   ```

4. **Access Swagger**:
   Visit `http://localhost:<service-port>/swagger-ui.html` for API testing.

---

## **Deployment**
### **1. Docker Compose**
Use `docker-compose.yml` for local deployment:
```yaml
version: '3'
services:
  auth-service:
    image: auth-service:latest
    ports:
      - "8081:8080"
  task-service:
    image: task-service:latest
    ports:
      - "8082:8080"
  ...
```

### **2. Kubernetes Deployment**
Deploy to AKS using YAML configurations:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: task-service
spec:
  replicas: 3
  template:
    spec:
      containers:
      - name: task-service
        image: task-service:latest
...
```

---

## **Testing**
Run unit and integration tests with Maven:
```bash
./mvnw test
```

---

## **Monitoring**
- **Spring Boot Actuator**:  
  Access health checks at `/actuator/health`.  
- **Elasticsearch**:  
  Query logs and metrics with:
  ```json
  {
    "query": { "match_all": {} }
  }
  ```

---

## **Troubleshooting**
- **Kafka Errors**: Ensure Kafka brokers are running and accessible.  
- **MongoDB Connection Issues**: Verify database URI and credentials.  
- **Keycloak Authentication**: Check client configurations in Keycloak admin console.

---

## Future Enhancements**
- Integrate Redis caching for faster task retrieval.  
- Add a mobile-friendly frontend.  
- Implement gRPC for inter-service communication.

---

## **Contributing**
1. Fork the repository.  
2. Create a feature branch:
   ```bash
   git checkout -b feature/new-feature
   ```
3. Commit changes and create a pull request.

---

## **License**
MIT License. 