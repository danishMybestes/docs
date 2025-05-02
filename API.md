# API Documentation

This document provides a comprehensive overview of all APIs used in the MyBestes application, their purposes, and their integration points.

## Table of Contents
1. [API Architecture Overview](#api-architecture-overview)
2. [API Groups](#api-groups)
3. [API Flow Diagrams](#api-flow-diagrams)
4. [API Usage Map](#api-usage-map)
5. [API Security](#api-security)
6. [API Error Handling](#api-error-handling)

## API Architecture Overview

```mermaid
graph TD
    A[Client App] --> B[API Manager]
    B --> C[Firebase Functions]
    C --> D[External APIs]
    D --> E[Google APIs]
    D --> F[OpenAI APIs]
    D --> G[WebWilli API]
    D --> H[Meta Conversion API]
    D --> I[Skinscreener API]
```

## API Groups

### 1. Google APIs Group
```mermaid
graph TD
    A[Google APIs] --> B[Maps API]
    A --> C[Places API]
    A --> D[Weather API]
    B --> B1[Autocomplete]
    B --> B2[Reverse Geocoding]
    C --> C1[Text Search]
    D --> D1[Weather Conditions]
```

| API | Endpoint | Purpose | Authentication |
|-----|----------|---------|----------------|
| Google Maps | /place/autocomplete/json | Location search autocomplete | API Key |
| Google Maps | /geocode/json | Reverse geocoding | API Key |
| Google Places | /places:searchText | Place search | API Key |
| Google Weather | /currentConditions:lookup | Weather data | API Key |

### 2. OpenAI APIs Group
```mermaid
graph TD
    A[OpenAI APIs] --> B[Chat Completions]
    A --> C[Vision]
    B --> B1[Text Analysis]
    C --> C1[Image Analysis]
```

| API | Endpoint | Purpose | Authentication |
|-----|----------|---------|----------------|
| Chat Completions | /chat/completions | Text analysis | Bearer Token |
| Vision | /chat/completions | Image analysis | Bearer Token |

### 3. Health APIs Group
```mermaid
graph TD
    A[Health APIs] --> B[Skinscreener]
    A --> C[WebWilli]
    B --> B1[Medical Image Analysis]
    C --> C1[Appointment Booking]
```

| API | Endpoint | Purpose | Authentication |
|-----|----------|---------|----------------|
| Skinscreener | /v1-med/images | Medical image analysis | API Key |
| WebWilli | /browse | Appointment booking | Bearer Token |

### 4. Analytics APIs Group
```mermaid
graph TD
    A[Analytics APIs] --> B[Meta Conversion]
    B --> B1[User Registration]
    B --> B2[Event Tracking]
```

| API | Endpoint | Purpose | Authentication |
|-----|----------|---------|----------------|
| Meta Conversion | /events | User registration tracking | Access Token |

## API Flow Diagrams

### 1. Health Cam Processing Flow
```mermaid
sequenceDiagram
    participant User
    participant App
    participant Firebase
    participant OpenAI
    participant Storage
    
    User->>App: Take Photo
    App->>Storage: Upload Image
    App->>Firebase: Request Analysis
    Firebase->>OpenAI: Vision API Call
    OpenAI-->>Firebase: Analysis Result
    Firebase-->>App: Processed Data
    App-->>User: Show Results
```

### 2. Location Services Flow
```mermaid
sequenceDiagram
    participant User
    participant App
    participant Firebase
    participant Google Maps
    
    User->>App: Search Location
    App->>Firebase: Request Location Data
    Firebase->>Google Maps: Places API
    Google Maps-->>Firebase: Location Data
    Firebase-->>App: Processed Data
    App-->>User: Show Results
```

## API Usage Map

```mermaid
graph LR
    subgraph Client Layer
        A[UI Components]
        B[State Management]
    end
    
    subgraph API Layer
        C[API Manager]
        D[Firebase Functions]
    end
    
    subgraph External Services
        E[Google APIs]
        F[OpenAI]
        G[Health APIs]
        H[Analytics]
    end
    
    A --> B
    B --> C
    C --> D
    D --> E
    D --> F
    D --> G
    D --> H
```

## API Security

### Authentication Flow
```mermaid
sequenceDiagram
    participant Client
    participant Firebase
    participant External API
    
    Client->>Firebase: Request API Access
    Firebase->>Firebase: Verify Token
    Firebase->>External API: Forward Request
    External API-->>Firebase: Response
    Firebase-->>Client: Processed Response
```

### Security Measures
1. **Token-based Authentication**
   - Firebase Authentication for user verification
   - API keys for external services
   - Bearer tokens for sensitive operations

2. **Data Protection**
   - HTTPS for all API calls
   - Encrypted payloads
   - Secure token storage

## API Error Handling

### Error Flow
```mermaid
graph TD
    A[API Call] --> B{Success?}
    B -->|Yes| C[Process Response]
    B -->|No| D[Error Handling]
    D --> E[Log Error]
    D --> F[User Notification]
    D --> G[Retry Logic]
```

### Error Categories
| Error Type | Handling Strategy | User Feedback |
|------------|-------------------|---------------|
| Authentication | Token refresh | Login prompt |
| Network | Retry mechanism | Connection error |
| API Limit | Rate limiting | Service unavailable |
| Validation | Input correction | Invalid input |
| Server | Fallback data | Service error |

## Best Practices

1. **API Call Management**
   - Implement caching where appropriate
   - Use retry mechanisms for failed calls
   - Monitor API usage and limits

2. **Performance Optimization**
   - Batch requests when possible
   - Implement request queuing
   - Use streaming for large data

3. **Error Handling**
   - Implement comprehensive error logging
   - Provide meaningful error messages
   - Handle edge cases gracefully

4. **Security**
   - Regular token rotation
   - Secure API key storage
   - Input validation
