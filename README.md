# Health & Wellness App API Documentation

## Base URL
```
https://api.healthwellnessapp.com/v1
```

## Authentication
All API requests require authentication using a Bearer token in the Authorization header:
```
Authorization: Bearer <your_token>
```

## Endpoints

### User Management

#### Get User Profile
```http
GET /users/profile
```
Response:
```json
{
  "id": "user123",
  "name": "John Doe",
  "email": "john@example.com",
  "profilePicture": "https://example.com/profile.jpg",
  "healthScore": 85,
  "createdAt": "2024-01-01T00:00:00Z"
}
```

#### Update User Profile
```http
PUT /users/profile
```
Request Body:
```json
{
  "name": "John Doe",
  "profilePicture": "base64encodedimage",
  "healthPreferences": {
    "notifications": true,
    "reminders": true
  }
}
```

### Health Monitoring

#### Get Health Metrics
```http
GET /health/metrics
```
Query Parameters:
- `startDate`: YYYY-MM-DD
- `endDate`: YYYY-MM-DD
- `type`: ["steps", "heart_rate", "sleep"]

Response:
```json
{
  "metrics": [
    {
      "date": "2024-03-31",
      "steps": 8500,
      "heartRate": 72,
      "sleepHours": 7.5
    }
  ]
}
```

### Challenges

#### Get Active Challenges
```http
GET /challenges
```
Response:
```json
{
  "challenges": [
    {
      "id": "challenge123",
      "title": "30-Day Fitness Challenge",
      "description": "Complete daily workouts for 30 days",
      "startDate": "2024-04-01",
      "endDate": "2024-04-30",
      "participants": 150,
      "progress": 45
    }
  ]
}
```

#### Join Challenge
```http
POST /challenges/{challengeId}/join
```
Response:
```json
{
  "success": true,
  "message": "Successfully joined the challenge"
}
```

### Appointments

#### Schedule Appointment
```http
POST /appointments
```
Request Body:
```json
{
  "type": "consultation",
  "date": "2024-04-15",
  "time": "14:30",
  "doctorId": "doc123",
  "notes": "Follow-up consultation"
}
```

#### Get Appointments
```http
GET /appointments
```
Query Parameters:
- `startDate`: YYYY-MM-DD
- `endDate`: YYYY-MM-DD

Response:
```json
{
  "appointments": [
    {
      "id": "appt123",
      "type": "consultation",
      "date": "2024-04-15",
      "time": "14:30",
      "doctor": {
        "id": "doc123",
        "name": "Dr. Smith",
        "specialty": "General Medicine"
      },
      "status": "scheduled"
    }
  ]
}
```

### Chat

#### Send Message
```http
POST /chat/messages
```
Request Body:
```json
{
  "recipientId": "user456",
  "message": "Hello, how are you?",
  "type": "text"
}
```

#### Get Chat History
```http
GET /chat/history/{userId}
```
Query Parameters:
- `limit`: number of messages to return
- `before`: timestamp for pagination

Response:
```json
{
  "messages": [
    {
      "id": "msg123",
      "senderId": "user123",
      "recipientId": "user456",
      "message": "Hello, how are you?",
      "timestamp": "2024-03-31T15:30:00Z"
    }
  ]
}
```

### Health Documents

#### Upload Document
```http
POST /documents
```
Request Body (multipart/form-data):
- `file`: document file
- `type`: ["medical_report", "prescription", "lab_result"]
- `description`: string

Response:
```json
{
  "id": "doc123",
  "url": "https://example.com/documents/doc123.pdf",
  "uploadedAt": "2024-03-31T16:00:00Z"
}
```

#### Get Documents
```http
GET /documents
```
Response:
```json
{
  "documents": [
    {
      "id": "doc123",
      "type": "medical_report",
      "description": "Annual checkup results",
      "url": "https://example.com/documents/doc123.pdf",
      "uploadedAt": "2024-03-31T16:00:00Z"
    }
  ]
}
```

### Family Management

#### Add Family Member
```http
POST /family/members
```
Request Body:
```json
{
  "name": "Jane Doe",
  "relationship": "spouse",
  "email": "jane@example.com",
  "permissions": ["view_health_data", "schedule_appointments"]
}
```

#### Get Family Members
```http
GET /family/members
```
Response:
```json
{
  "members": [
    {
      "id": "member123",
      "name": "Jane Doe",
      "relationship": "spouse",
      "permissions": ["view_health_data", "schedule_appointments"]
    }
  ]
}
```

## Error Responses

All API endpoints may return the following error responses:

### 400 Bad Request
```json
{
  "error": "Invalid request parameters",
  "message": "Detailed error message"
}
```

### 401 Unauthorized
```json
{
  "error": "Unauthorized",
  "message": "Invalid or expired token"
}
```

### 404 Not Found
```json
{
  "error": "Resource not found",
  "message": "The requested resource does not exist"
}
```

### 500 Internal Server Error
```json
{
  "error": "Internal server error",
  "message": "An unexpected error occurred"
}
```

## Rate Limiting
- Free tier: 100 requests per hour
- Premium tier: 1000 requests per hour
- Enterprise tier: 10000 requests per hour

Rate limit headers are included in all responses:
```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1625097600
```
