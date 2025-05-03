# Conduit MVP Scope Document

This document outlines the scope, features, and implementation plan for the Minimum Viable Product (MVP) of Conduit, a note aggregation platform. The MVP is targeted for completion by July 16th, 2025, spanning 5 two-week sprints.

## 1. MVP Overview

Conduit's MVP will deliver a web-based Progressive Web App (PWA) that allows users to create, organize, search, and manage text notes with rich formatting. The system will support importing and exporting notes in various text formats and provide a hierarchical organization system with both folders and tags.

### Core Value Proposition

The MVP will solve the fundamental problem of scattered notes by providing:
- A centralized repository for text-based notes
- Consistent organization through folders and tags
- Full-text search across all notes
- Import/export capabilities for common text formats
- Multi-user support with basic authentication

## 2. Feature Specifications

### 2.1 Platform: Web-First PWA

- **Single-page application (SPA)** with responsive design
- **Progressive Web App features**:
  - Basic offline access to recently viewed notes
  - Installable on devices
  - Background sync when connection is restored
- **Browser compatibility**: Focus on modern browsers (Chrome, Firefox, Safari, Edge)

### 2.2 Note Management

- **Rich text editor** with common formatting options:
  - Bold, italic, underline, headings
  - Bulleted and numbered lists
  - Links
  - Code blocks
- **Note metadata**:
  - Title
  - Creation timestamp
  - Last modified timestamp
  - Edit count
  - User who last modified
  - Associated tags
  - Parent folder
- **Basic audit logging**:
  - Track creation and modification timestamps
  - Record edit counts
  - Log user who made changes

### 2.3 Organization System

- **Hierarchical folder structure**:
  - Unlimited nesting capability
  - VSCode-like collapsible tree view
  - Create, rename, delete, and move folders
- **Tagging system**:
  - Create, edit, delete tags
  - Assign multiple tags to notes
  - Filter notes by tag
- **Basic sorting and filtering**:
  - Sort by name, creation date, modified date
  - Filter by folder, tag, or both

### 2.4 Search Functionality

- **Full-text search** across all notes
- **Search within** specific folders or with specific tags
- **Highlight matching terms** in results
- **Recent searches** history
- **Performance considerations**:
  - Server-side indexed search using Elasticsearch

### 2.5 Import/Export Capabilities

- **Import formats**:
  - Markdown (.md)
  - Plain text (.txt)
  - Rich Text Format (.rtf)
  - Word documents (.docx)
  - PDF text extraction (.pdf)
- **Export formats**:
  - Same as import formats
- **Batch operations**:
  - Import multiple files at once
  - Export multiple notes as separate files

### 2.6 Authentication & Security

- **User authentication**:
  - Email/password registration and login
  - Password reset functionality
  - Session management
- **Multi-user support**:
  - User-specific notes and folders
  - No sharing/collaboration features in MVP
- **Basic security**:
  - Encrypted passwords
  - HTTPS connections
  - Input validation and sanitization

## 3. Technical Stack

### 3.1 Frontend

- **Framework**: React.js
- **State Management**: Redux
- **UI Library**: Material-UI or Chakra UI
- **Rich Text Editor**: Quill.js or TinyMCE
- **PWA Support**: Workbox (for service workers and offline capabilities)
- **Hosting**: Vercel

### 3.2 Backend

- **API Framework**: Node.js with Express
- **Authentication**: Passport.js
- **File Processing**: Multer with appropriate parsers
- **Hosting**: Fly.io

### 3.3 Data Storage

- **Database**: MongoDB Atlas
- **Search**: Elasticsearch Cloud

## 4. Data Schema Design

### 4.1 Note Schema

```javascript
{
  id: String,                // Unique identifier
  title: String,             // Note title
  content: String,           // Rich text content (HTML or JSON format)
  format: String,            // Format type (markdown, rich text)
  createdAt: Date,           // Creation timestamp
  updatedAt: Date,           // Last update timestamp
  editCount: Number,         // Number of edits
  createdBy: String,         // User ID of creator
  lastEditedBy: String,      // User ID of last editor
  folderId: String,          // Parent folder ID
  tags: [String],            // Array of tag IDs
  sourceFormat: String,      // Original format if imported
  sourceFile: String,        // Original filename if imported
}
```

### 4.2 Folder Schema

```javascript
{
  id: String,                // Unique identifier
  name: String,              // Folder name
  parentId: String,          // Parent folder ID (null for root)
  createdAt: Date,           // Creation timestamp
  updatedAt: Date,           // Last update timestamp
  userId: String,            // Owner user ID
  path: String,              // Full path for easier navigation
}
```

### 4.3 Tag Schema

```javascript
{
  id: String,                // Unique identifier
  name: String,              // Tag name
  color: String,             // Color code (hex)
  createdAt: Date,           // Creation timestamp
  updatedAt: Date,           // Last update timestamp
  userId: String,            // Owner user ID
}
```

### 4.4 User Schema

```javascript
{
  id: String,                // Unique identifier
  email: String,             // User email
  passwordHash: String,      // Hashed password
  name: String,              // User's display name
  createdAt: Date,           // Account creation timestamp
  lastLogin: Date,           // Last login timestamp
  preferences: {             // User preferences
    defaultView: String,     // Default view mode
    theme: String,           // UI theme preference
    // Other preferences
  }
}
```

## 5. Development Approach

### 5.1 Sprint 1 (May 7-21): Foundation

- **Create detailed specifications** for authentication, data schemas, and basic note functionality
- Set up project structure and repositories
- Implement basic authentication with Passport.js
- Define data schemas
- Create basic API endpoints
- Implement simple note creation and editing (plain text initially)
- Establish basic folder structure

**Key Deliverables:**
- Working authentication system
- Basic note CRUD operations
- Initial database setup

### 5.2 Sprint 2 (May 22-June 4): Core Functionality

- **Create detailed specifications** for rich text editing, tagging system, and folder visualization
- Implement rich text editing
- Develop tagging system
- Create folder hierarchy visualization
- Basic search functionality
- Note rendering components

**Key Deliverables:**
- Rich text editor integration
- Folder and tag management UI
- Basic search implementation

### 5.3 Sprint 3 (June 5-18): Organization & Search

- **Create detailed specifications** for search integration, filtering, and folder explorer
- Enhance search with Elasticsearch integration
- Implement sorting and advanced filtering
- Improve folder/tag UI and interactions
- Add audit logging for notes
- Implement VSCode-like folder explorer

**Key Deliverables:**
- Full-text search across notes
- Complete organization system
- Audit logging functionality

### 5.4 Sprint 4 (June 19-July 2): Import/Export & PWA

- **Create detailed specifications** for import/export functionality and PWA features
- Implement file import functionality
- Add export capabilities
- Set up PWA features
- Begin offline capabilities
- Implement batch operations

**Key Deliverables:**
- Working import/export system
- PWA configuration
- Basic offline functionality

### 5.5 Sprint 5 (July 3-16): Polish & Testing

- **Create detailed specifications** for UI improvements and performance optimizations
- Improve UI/UX based on initial feedback
- Enhance performance
- Fix bugs
- Conduct user testing
- Prepare for deployment

**Key Deliverables:**
- Polished user interface
- Performance optimizations
- Deployment-ready application

## 6. Development Priorities

1. **Note Schema & Rendering**: Define what constitutes a note and how it's displayed
2. **Authentication**: Implement user accounts and security
3. **Core CRUD Operations**: Create, read, update, delete notes
4. **Organization System**: Implement folders and tags
5. **Search Functionality**: Implement full-text search
6. **Import/Export**: Add file processing capabilities
7. **PWA Features**: Implement offline access and installability
8. **UI Polish**: Refine the user experience

## 7. Success Criteria

The MVP will be considered successful if it:

1. Allows users to create, edit, organize, and find notes efficiently
2. Supports importing notes from at least 3 common formats
3. Provides reliable full-text search across all notes
4. Functions on both desktop and mobile web browsers
5. Maintains acceptable performance with 100+ notes per user
6. Receives positive feedback from initial user testing

## 8. Out of Scope for MVP

The following features are explicitly out of scope for the MVP:

1. Real-time collaboration
2. OCR for handwritten notes
3. Image and whiteboard capture
4. Advanced AI-based organization
5. Mobile native applications
6. Third-party integrations (beyond file import)
7. Sharing and permissions system
8. Advanced version history (beyond basic audit logging)

These features will be considered for future releases after the MVP is successfully launched.

## 9. Technical Considerations

### 9.1 Performance

- Implement pagination for note lists
- Use server-side search for efficiency
- Optimize rich text rendering
- Consider lazy loading for folder structures

### 9.2 Security

- Implement proper authentication with Passport.js
- Sanitize user inputs to prevent XSS
- Use HTTPS for all communications
- Implement proper validation on all API endpoints

### 9.3 Scalability

- Design database schemas with indexing in mind
- Structure the application for horizontal scaling
- Use efficient search indexing with Elasticsearch

## 10. Development Specification Approach

### Just-in-Time Specification Strategy

Rather than creating exhaustive detailed specifications for all components upfront, Conduit will use a "just-in-time" specification approach:

1. **This MVP scope document** serves as the foundation and high-level guide
2. **Detailed specifications** will be created immediately before implementing each component
3. **Sprint-by-sprint focus** - create detailed specs only for components in the current sprint

This approach offers several benefits:
- Prevents wasting time on specs that might change as development progresses
- Allows for learning and adjustment throughout the development process
- Keeps documentation aligned with actual implementation
- Focuses energy on what's immediately needed

**IMPORTANT NOTE FOR DEVELOPMENT AGENT**: Each sprint should begin with creating detailed specifications for the components to be implemented in that sprint. These specifications should include:
- API endpoint definitions where applicable
- UI wireframes or mockups
- Detailed workflow diagrams
- Edge cases and error handling
- Specific implementation details for the chosen technologies

## 11. Next Steps

1. Set up development environment and project structure
2. Establish Git repositories and CI/CD pipelines
3. Begin implementation according to Sprint 1 plan
4. Schedule regular progress reviews and adjustments
