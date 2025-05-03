# Technical Context: Conduit Note Aggregator

## Technologies Used

Conduit leverages a modern technology stack designed for scalability, maintainability, and developer productivity. The following technologies have been selected for the project:

### Frontend Technologies

#### Web Application
- **Framework**: React.js with TypeScript
- **State Management**: Redux for global state
- **UI Library**: Material-UI or Chakra UI
- **Rich Text Editor**: Quill.js or TinyMCE
- **PWA Support**: Workbox (for service workers and offline capabilities)
- **Build Tools**: Webpack, Babel
- **Testing**: Jest, React Testing Library
- **Hosting**: Vercel

#### Future Mobile Applications (Post-MVP)
- **Framework**: React Native or Flutter
- **State Management**: Redux or MobX
- **UI Components**: Native components with custom styling
- **Navigation**: React Navigation (if using React Native)

#### Future Desktop Applications (Post-MVP)
- **Framework**: Electron
- **Core**: Same React codebase as web with platform-specific adaptations

### Backend Technologies

#### API Layer
- **Framework**: Node.js with Express
- **API Types**: 
  - REST API with Express
  - GraphQL API with Apollo Server
- **Authentication**: Passport.js, JWT
- **Validation**: Joi or Yup
- **Documentation**: Swagger/OpenAPI
- **Hosting**: Fly.io

#### Service Layer
- **Language**: JavaScript/TypeScript
- **Architecture**: Microservices
- **Communication**: REST, GraphQL, and Event-based
- **Testing**: Jest, Supertest
- **Containerization**: Docker
- **Orchestration**: Kubernetes (for post-MVP scaling)

#### Data Layer
- **Primary Database**: MongoDB Atlas (document database)
- **Search Engine**: Elasticsearch Cloud
- **Object Storage**: AWS S3 or equivalent
- **Caching**: Redis (for post-MVP performance optimization)
- **Database Access**: Mongoose ODM

### DevOps & Infrastructure
- **CI/CD**: GitHub Actions
- **Monitoring**: Prometheus, Grafana
- **Logging**: ELK Stack or Cloud-based logging solution
- **Infrastructure as Code**: Terraform
- **Environment Management**: Docker Compose for development

## Development Setup

### Local Development Environment

#### Prerequisites
- Node.js (v16+)
- npm or Yarn
- Docker and Docker Compose
- MongoDB (local or containerized)
- Elasticsearch (local or containerized)
- Git

#### Repository Structure
```
conduit/
├── client/               # Frontend application
│   ├── public/           # Static assets
│   ├── src/              # React source code
│   │   ├── components/   # UI components
│   │   ├── pages/        # Page components
│   │   ├── services/     # API client services
│   │   ├── store/        # Redux store
│   │   └── utils/        # Utility functions
│   ├── tests/            # Frontend tests
│   └── package.json      # Frontend dependencies
├── server/               # Backend services
│   ├── src/              # Source code
│   │   ├── api/          # API definitions
│   │   ├── services/     # Service implementations
│   │   ├── models/       # Data models
│   │   ├── utils/        # Utility functions
│   │   └── config/       # Configuration
│   ├── tests/            # Backend tests
│   └── package.json      # Backend dependencies
├── docker/               # Docker configuration
│   ├── docker-compose.yml # Local development setup
│   └── Dockerfile.*      # Service-specific Dockerfiles
├── docs/                 # Documentation
└── package.json          # Root package.json for scripts
```

#### Setup Process
1. Clone the repository
2. Install dependencies with `npm install` or `yarn`
3. Set up environment variables (see Environment Configuration)
4. Start the development environment with `docker-compose up`
5. Access the application at `http://localhost:3000`

#### Environment Configuration
- `.env.development` - Development environment variables
- `.env.test` - Test environment variables
- `.env.production` - Production environment variables

Key environment variables include:
- `MONGODB_URI` - MongoDB connection string
- `ELASTICSEARCH_URL` - Elasticsearch endpoint
- `JWT_SECRET` - Secret for JWT token generation
- `S3_BUCKET` - S3 bucket for file storage
- `API_URL` - Backend API URL for frontend

### Development Workflow

#### Branching Strategy
- `main` - Production-ready code
- `develop` - Integration branch for features
- `feature/*` - Feature branches
- `bugfix/*` - Bug fix branches
- `release/*` - Release preparation branches

#### Commit Conventions
- Follow Conventional Commits format
- Use semantic prefixes (feat, fix, docs, style, refactor, test, chore)
- Reference issue numbers in commit messages

#### Pull Request Process
1. Create feature branch from `develop`
2. Implement changes with tests
3. Submit PR to `develop`
4. Code review by at least one team member
5. Pass CI checks (linting, tests, build)
6. Merge to `develop`

#### Deployment Pipeline
1. Merge to `develop` triggers deployment to development environment
2. Release branch creation triggers deployment to staging
3. Merge to `main` triggers deployment to production
4. Automated tests run at each stage

## Technical Constraints

### Performance Requirements
- **Page Load Time**: < 2 seconds for initial load
- **Search Response Time**: < 500ms for typical queries
- **Note Save Time**: < 1 second
- **Concurrent Users**: Support for 1000+ concurrent users in production

### Scalability Considerations
- Horizontal scaling of services
- Database sharding for large user bases
- CDN for static assets
- Caching strategy for frequently accessed data

### Security Requirements
- HTTPS for all communications
- JWT-based authentication
- Password hashing with bcrypt
- Input validation and sanitization
- CSRF protection
- Rate limiting for API endpoints
- Regular security audits

### Compliance Considerations
- GDPR compliance for user data
- Data portability (export functionality)
- Proper data deletion mechanisms
- Privacy policy implementation

### Browser & Device Support
- **Desktop**: Chrome, Firefox, Safari, Edge (latest 2 versions)
- **Mobile**: iOS Safari, Android Chrome (latest 2 versions)
- **Minimum Screen Size**: 320px width (mobile)
- **Responsive Design**: Support for all screen sizes

## Dependencies & External Services

### Third-Party Libraries
- **Frontend Core**: React, Redux, React Router
- **UI Components**: Material-UI or Chakra UI
- **Rich Text Editing**: Quill.js or TinyMCE
- **Data Fetching**: Axios or fetch API
- **Form Handling**: Formik or React Hook Form
- **Validation**: Yup or Joi
- **Date Handling**: date-fns or Luxon
- **Utilities**: Lodash (selective imports)

### External Services
- **Authentication**: Potentially Auth0 or Firebase Auth (TBD)
- **Database**: MongoDB Atlas
- **Search**: Elasticsearch Cloud
- **Storage**: AWS S3 or equivalent
- **Monitoring**: Datadog or New Relic
- **Error Tracking**: Sentry
- **Analytics**: Google Analytics or Mixpanel

### Integration Points
- **Notion API**: For importing notes from Notion
- **Microsoft Graph API**: For OneNote integration
- **Google Drive API**: For Google Docs integration
- **iCloud API**: For iCloud Notes integration
- **OCR Service**: For processing images of handwritten notes

## Tool Usage Patterns

### Development Tools
- **IDE**: VS Code with recommended extensions
- **API Testing**: Postman or Insomnia
- **Database Management**: MongoDB Compass
- **Version Control**: Git with GitHub
- **Package Management**: npm or Yarn
- **Documentation**: Markdown, Storybook for components

### Testing Approach
- **Unit Testing**: Jest for both frontend and backend
- **Component Testing**: React Testing Library
- **API Testing**: Supertest
- **E2E Testing**: Cypress
- **Test Coverage**: Aim for 80%+ coverage
- **TDD Workflow**: Encouraged for critical components

### Monitoring & Debugging
- **Logging**: Structured JSON logs
- **Log Levels**: ERROR, WARN, INFO, DEBUG
- **Performance Monitoring**: Datadog or New Relic
- **Error Tracking**: Sentry for frontend and backend
- **Alerting**: Based on error rates and performance thresholds

## MVP Technical Focus

For the MVP phase, the technical focus will be on:

1. **Web Application**: Fully functional React PWA
2. **Core Backend Services**: Authentication, Notes, Search
3. **Basic Data Storage**: MongoDB and Elasticsearch
4. **Essential APIs**: REST API for core functionality
5. **Import/Export**: Basic file format support
6. **Offline Capabilities**: PWA with basic offline access

This foundation will establish the core technical infrastructure while setting the stage for more advanced features and additional platforms in future phases.
