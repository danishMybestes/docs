# Actions Documentation

This document provides a detailed overview of all actions used in the MyBestes application, their purposes, and their relationships within the application architecture.

## Table of Contents
1. [Action Categories](#action-categories)
2. [Action Flow Diagrams](#action-flow-diagrams)
3. [Action Dependencies](#action-dependencies)
4. [Action Usage Map](#action-usage-map)
5. [Action Architecture](#action-architecture)

## Action Categories

### 1. User Interface Actions
```mermaid
graph TD
    A[UI Actions] --> B[Snackbar Actions]
    A --> C[Dialog Actions]
    A --> D[Theme Actions]
    B --> B1[notAvailableSnackbar]
    B --> B2[checkInternetConnection]
    C --> C1[showDialog]
    D --> D1[setThemeMode]
```

### 2. Content Management Actions
```mermaid
graph TD
    A[Content Actions] --> B[Video Actions]
    A --> C[Feed Actions]
    B --> B1[resetContentVideo]
    C --> C1[updateFeedItem]
    C --> C2[createFeedItem]
```

### 3. Health Cam Actions
```mermaid
graph TD
    A[Health Cam] --> B[Image Processing]
    A --> C[AI Analysis]
    A --> D[Data Storage]
    B --> B1[base64DataUrlFromImageUrl]
    C --> C1[visionCall]
    D --> D1[createCamRecord]
    D --> D2[createFeedItem]
```

### 4. Authentication Actions
```mermaid
graph TD
    A[Auth Actions] --> B[Session Management]
    A --> C[User Management]
    B --> B1[startSession]
    B --> B2[endSession]
    C --> C1[updateUserProfile]
    C --> C2[verifyEmail]
```

## Action Flow Diagrams

### 1. Health Cam Processing Flow
```mermaid
sequenceDiagram
    participant User
    participant App
    participant AI
    participant Database
    
    User->>App: Take Photo
    App->>App: base64DataUrlFromImageUrl
    App->>AI: visionCall
    AI-->>App: Analysis Result
    App->>Database: createCamRecord
    App->>Database: createFeedItem
    App-->>User: Show Results
```

### 2. User Session Flow
```mermaid
sequenceDiagram
    participant User
    participant App
    participant Auth
    participant Database
    
    User->>App: Login
    App->>Auth: Authenticate
    Auth-->>App: Success
    App->>Database: startSession
    App->>Database: updateUserProfile
    App-->>User: Show Dashboard
```

## Action Dependencies

| Action | Dependencies | Used By |
|--------|-------------|---------|
| notAvailableSnackbar | FlutterFlowTheme, BuildContext | UI Components |
| resetContentVideo | FFAppState | Video Player |
| checkInternetConnection | Internet Connection Service | Network Operations |
| runHealthCam | OpenAI API, Firebase | Health Cam Feature |
| startSession | Firebase Auth | Authentication System |

## Action Usage Map

```mermaid
graph LR
    subgraph UI Layer
        A[Snackbars]
        B[Dialogs]
        C[Themes]
    end
    
    subgraph Business Layer
        D[Health Cam]
        E[Content]
        F[Auth]
    end
    
    subgraph Data Layer
        G[Firebase]
        H[Local Storage]
    end
    
    A --> D
    B --> E
    C --> F
    D --> G
    E --> G
    F --> G
    F --> H
```

## Action Architecture

### 1. Layer Architecture
```mermaid
graph TD
    subgraph Presentation Layer
        A[UI Actions]
        B[State Management]
    end
    
    subgraph Domain Layer
        C[Business Logic]
        D[Validation]
    end
    
    subgraph Data Layer
        E[API Calls]
        F[Database Operations]
    end
    
    A --> B
    B --> C
    C --> D
    D --> E
    D --> F
```

### 2. Action Categories and Their Responsibilities

| Category | Responsibilities | Example Actions |
|----------|-----------------|----------------|
| UI Actions | Handle user interface interactions | notAvailableSnackbar, showDialog |
| Content Actions | Manage content display and updates | resetContentVideo, updateFeedItem |
| Health Actions | Process health-related data | runHealthCam, processHealthData |
| Auth Actions | Handle authentication and sessions | startSession, verifyEmail |

### 3. Action State Management

```mermaid
stateDiagram-v2
    [*] --> Idle
    Idle --> Processing: Action Triggered
    Processing --> Success: Action Completed
    Processing --> Error: Action Failed
    Success --> Idle: Reset State
    Error --> Idle: Reset State
```

## Best Practices

1. **Action Naming Conventions**
   - Use clear, descriptive names
   - Follow camelCase convention
   - Include action category in name (e.g., `showSnackbar`, `updateUserProfile`)

2. **Error Handling**
   - Always implement error handling
   - Provide user feedback
   - Log errors appropriately

3. **State Management**
   - Use FFAppState for global state
   - Implement proper state cleanup
   - Handle state persistence

4. **Performance Considerations**
   - Minimize API calls
   - Implement caching where appropriate
   - Use background processing for heavy operations

## Security Considerations

1. **Authentication**
   - Always verify user authentication
   - Implement proper session management
   - Use secure storage for sensitive data

2. **Data Protection**
   - Encrypt sensitive data
   - Implement proper access control
   - Follow data protection regulations

## Future Improvements

1. **Action Optimization**
   - Implement action caching
   - Add retry mechanisms
   - Improve error recovery

2. **New Features**
   - Add offline support
   - Implement action queuing
   - Add action analytics

3. **Documentation**
   - Add more detailed flow diagrams
   - Include performance metrics
   - Document edge cases
