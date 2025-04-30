# MyBestes - Project Architecture Overview

## 1. Project Structure

```mermaid
graph TD
    A[MyBestes] --> B[lib]
    A --> C[assets]
    A --> D[firebase]
    A --> E[dependencies]
    
    B --> B1[auth]
    B --> B2[main_feed]
    B --> B3[values]
    B --> B4[admin]
    B --> B5[common]
    B --> B6[backend]
    
    C --> C1[images]
    C --> C2[videos]
    C --> C3[audios]
    C --> C4[fonts]
    C --> C5[pdfs]
    C --> C6[rive_animations]
```

## 2. Core Features & Modules

### 2.1 Authentication System
- **Components**:
  - Login/Register forms
  - Social auth integration
  - Password reset
  - Profile management

```mermaid
sequenceDiagram
    participant User
    participant App
    participant Firebase
    participant Social
    
    User->>App: Login Request
    App->>Firebase: Authenticate
    Firebase-->>App: Auth Token
    App->>Social: Social Login
    Social-->>App: Social Token
    App->>Firebase: Verify Token
    Firebase-->>App: User Data
    App-->>User: Access Granted
```

### 2.2 Main Feed
- **Components**:
  - Feed items
  - Content cards
  - Interactive elements
  - User engagement widgets

```mermaid
graph TD
    A[Main Feed] --> B[Content Types]
    B --> B1[Posts]
    B --> B2[Videos]
    B --> B3[Challenges]
    B --> B4[Questions]
    
    A --> C[User Actions]
    C --> C1[Like]
    C --> C2[Comment]
    C --> C3[Share]
    C --> C4[Save]
```

### 2.3 Values System
- **Components**:
  - Weight tracking
  - Sport activities
  - Mood monitoring
  - Sin tracking

```mermaid
graph LR
    A[Values] --> B[Health]
    A --> C[Activity]
    A --> D[Emotional]
    A --> E[Behavioral]
    
    B --> B1[Weight]
    C --> C1[Sport]
    D --> D1[Mood]
    E --> E1[Sin]
```

## 3. Firebase Schema

### 3.1 Collections Structure
```mermaid
erDiagram
    USERS {
        string uid
        string email
        string displayName
        string photoURL
        timestamp createdAt
    }
    
    CONTENT {
        string contentId
        string userId
        string type
        string title
        string description
        timestamp createdAt
    }
    
    VALUES {
        string valueId
        string userId
        string type
        number value
        timestamp createdAt
    }
    
    USERS ||--o{ CONTENT : creates
    USERS ||--o{ VALUES : tracks
```

## 4. Navigation Flow

```mermaid
graph TD
    A[Auth] --> B[Main Feed]
    B --> C[Values]
    B --> D[Challenges]
    B --> E[Profile]
    
    C --> C1[Weight]
    C --> C2[Sport]
    C --> C3[Mood]
    C --> C4[Sin]
    
    D --> D1[Active]
    D --> D2[Completed]
    D --> D3[New]
    
    E --> E1[Settings]
    E --> E2[History]
    E --> E3[Achievements]
```

## 5. Component Architecture

### 5.1 Widget Hierarchy
```mermaid
graph TD
    A[App] --> B[AuthWrapper]
    B --> C[MainFeed]
    B --> D[Values]
    B --> E[Admin]
    
    C --> C1[FeedItem]
    C --> C2[ContentCard]
    C --> C3[ActionBar]
    
    D --> D1[ValueInput]
    D --> D2[ValueHistory]
    D --> D3[ValueStats]
```

## 6. Dynamic Configurations

### 6.1 Feature Flags
```mermaid
graph TD
    A[Remote Config] --> B[Features]
    B --> B1[Social Login]
    B --> B2[Video Upload]
    B --> B3[Analytics]
    B --> B4[Notifications]
```

### 6.2 Content Rules
```mermaid
graph TD
    A[Content Rules] --> B[Validation]
    B --> B1[Text Length]
    B --> B2[Media Size]
    B --> B3[Format]
    
    A --> C[Moderation]
    C --> C1[Auto Filter]
    C --> C2[Manual Review]
```

## 7. State Management

```mermaid
graph TD
    A[App State] --> B[User State]
    A --> C[Content State]
    A --> D[Values State]
    
    B --> B1[Auth]
    B --> B2[Preferences]
    
    C --> C1[Feed]
    C --> C2[Cache]
    
    D --> D1[Current]
    D --> D2[History]
```

## 8. Asset Management

```mermaid
graph TD
    A[Assets] --> B[Media]
    A --> C[UI]
    A --> D[Data]
    
    B --> B1[Images]
    B --> B2[Videos]
    B --> B3[Audio]
    
    C --> C1[Fonts]
    C --> C2[Animations]
    
    D --> D1[Configs]
    D --> D2[Localization]
```

## 9. Security Implementation

```mermaid
graph TD
    A[Security] --> B[Auth]
    A --> C[Data]
    A --> D[Storage]
    
    B --> B1[Token]
    B --> B2[Session]
    
    C --> C1[Encryption]
    C --> C2[Validation]
    
    D --> D1[Access]
    D --> D2[Rules]
```

## 10. Error Handling

```mermaid
graph TD
    A[Error] --> B[Types]
    B --> B1[Network]
    B --> B2[Auth]
    B --> B3[Data]
    
    A --> C[Handling]
    C --> C1[Logging]
    C --> C2[User Feedback]
    C --> C3[Recovery]
```

This architecture document provides a high-level overview of your project's structure and components. Each section can be expanded with more detailed implementation specifics as needed.
