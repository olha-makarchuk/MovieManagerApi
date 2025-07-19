# 🎬 MovieManager System

This is a microservice-based system for managing movies in a cinema environment. It is built using .NET 8 and follows a clean architecture approach (Onion Architecture) with CQRS via MediatR, asynchronous messaging using RabbitMQ, and service-to-service communication over HttpClient.

---

## 🧱 Microservice Structure

| Service | Description |
|--------|-------------|
| **MovieManagerApi** | Main API for managing movies and cinema sessions |
| **CoreReferenceDataApi** | Reference data service (e.g., genres, directors) |
| **MovieSalesReportingApi** | Handles sales reporting via RabbitMQ |

---

## 🔧 Technologies Used

- **.NET 8**
- **ASP.NET Core Web API**
- **Entity Framework Core 8.0.4**
- **MediatR 12.2.0**
- **RabbitMQ**
- **AutoMapper 13.0.1**
- **Swagger** 
- **Newtonsoft.Json**
- **xUnit / Moq / FluentAssertions** for unit testing
- **Onion Architecture** for separation of concerns
- **Docker** for containerization
  
---

## 🚀 Getting Started

### 1️⃣ Clone the repository
    git clone https://github.com/olha-makarchuk/MovieManagerApi.git
    cd MovieManagerApi

### 2️⃣ Start RabbitMQ (optional via Docker)
    docker run -d --hostname rabbitmq --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3-management
  Access UI at: http://localhost:15672 (username: guest / password: guest)

### 3️⃣ Configure Databases
   For each microservice, run:
  
    dotnet ef database update --project [Your DAL Project]

   Example:
  
    dotnet ef database update --project Infrastructure/MovieManagerApi.Infrastructure.csproj

### 4️⃣ Run the services
    dotnet run --project MovieManagerApi/MovieManagerApi.csproj
    dotnet run --project CoreReferenceDataApi/CoreReferenceData.csproj
    dotnet run --project MovieSalesReportingApi/MovieSalesReporting.csproj

## 📬 Microservice Communication
MovieManagerApi ↔️ CoreReferenceDataApi via HttpClient

MovieManagerApi → MovieSalesReportingApi via RabbitMQ

## 🧪 Unit Testing
The project uses xUnit, Moq, and FluentAssertions for unit testing.

Run tests with:
```
dotnet test
```

### 📦 Dependency Management
Each microservice contains a dependencies.txt file, generated using:

```
dotnet list package > dependencies.txt
```
