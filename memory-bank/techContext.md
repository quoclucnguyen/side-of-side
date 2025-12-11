# Tech Context - Side of Side

## Technology Stack

### Core Framework
- **NestJS v11.0.1** - Progressive Node.js framework for building efficient server-side applications
- **TypeScript v5.7.3** - Static typing cho better code quality và developer experience

### Database & ORM
- **PostgreSQL v8.16.3** - Robust relational database
- **TypeORM v0.3.28** - TypeScript ORM với Active Record pattern
- **@nestjs/typeorm v11.0.0** - NestJS integration cho TypeORM

### API Documentation
- **@nestjs/swagger v11.2.3** - Automatic API documentation generation
- **Swagger UI** - Interactive API documentation

### Validation & Transformation
- **class-validator v0.14.3** - Decorator-based validation
- **class-transformer** - Object transformation (implicit dependency)

### Configuration Management
- **@nestjs/config v4.0.2** - Environment configuration management
- **Joi v18.0.2** - Schema validation cho environment variables

### Development Tools
- **@nestjs/cli v11.0.0** - Command-line interface cho NestJS
- **ESLint v9.18.0** - JavaScript/TypeScript linting
- **Prettier v3.4.2** - Code formatting
- **Jest v30.0.0** - Testing framework

### Additional Dependencies
- **reflect-metadata v0.2.2** - Required cho TypeScript decorators
- **rxjs v7.8.1** - Reactive programming (NestJS dependency)

## Development Setup

### Environment Configuration
```typescript
// Required environment variables
DATABASE_URL=postgresql://user:password@localhost:5432/dbname
PORT=3000
```

### Environment File Priority
1. `.env.development.local` (highest priority, git ignored)
2. `.env.development` 
3. `.env` (lowest priority)

### Database Configuration
- **Auto-load entities**: Enabled
- **Synchronize**: Enabled (development mode)
- **Logging**: Enabled (development mode)
- **Connection**: PostgreSQL via DATABASE_URL

## Project Structure

### Directory Layout
```
src/
├── app.module.ts          # Root module
├── app.controller.ts      # Root controller
├── app.service.ts         # Root service
├── main.ts               # Application entry point
└── users/                # Users feature module
    ├── users.module.ts
    ├── users.controller.ts
    ├── users.service.ts
    ├── dto/
    │   ├── create-user.dto.ts
    │   └── update-user.dto.ts
    └── entities/
        └── user.entity.ts
```

### Build Configuration
- **Build tool**: NestJS CLI (webpack-based)
- **Output directory**: `dist/`
- **Source maps**: Enabled cho debugging
- **Target**: ES2020

### Testing Configuration
- **Framework**: Jest
- **Test files**: `*.spec.ts`
- **Coverage**: Supported via `npm run test:cov`
- **E2E tests**: Located in `test/` directory

## Code Quality Tools

### ESLint Configuration
- **Config**: Modern flat config (eslint.config.mjs)
- **Preset**: @eslint/js + globals
- **Integration**: Prettier plugin for consistent formatting

### Prettier Configuration
- **Config**: .prettierrc
- **Target**: TypeScript files in src/ and test/
- **Integration**: ESLint plugin for seamless workflow

### TypeScript Configuration
- **Build config**: tsconfig.build.json
- **Development config**: tsconfig.json
- **Path mapping**: Support cho absolute imports
- **Strict mode**: Enabled

## Runtime Environment

### Node.js Requirements
- **Minimum**: Node.js 18.x (inferred from dependencies)
- **Recommended**: Latest LTS version
- **Package manager**: npm (package-lock.json present)

### Production Considerations
- **Process manager**: PM2 or Docker recommended
- **Environment variables**: Required cho production
- **Database**: PostgreSQL connection string required
- **Port**: Configurable via PORT environment variable

## Deployment Configuration

### Build Process
```bash
npm run build          # Build production assets
npm run start:prod     # Start production server
```

### Environment Variables cho Production
```bash
NODE_ENV=production
DATABASE_URL=postgresql://...
PORT=3000
```

### Docker Considerations
- **Base image**: node:18-alpine (recommended)
- **Working directory**: /app
- **Health check**: GET /health (future implementation)
- **Multi-stage build**: Optimize image size

## Development Workflow

### Local Development
```bash
npm install           # Install dependencies
npm run start:dev     # Start with hot reload
```

### Code Quality Workflow
```bash
npm run lint          # Run ESLint
npm run format        # Format code with Prettier
npm run test          # Run unit tests
npm run test:e2e      # Run E2E tests
```

### API Documentation
- **Access**: http://localhost:3000/api (when Swagger is configured)
- **Auto-generation**: Based on decorators in controllers và DTOs
- **Interactive testing**: Built-in Swagger UI

## Monitoring & Logging

### Current State
- **Database logging**: Enabled via TypeORM
- **Application logging**: NestJS default logger
- **Error handling**: Default NestJS exception filters

### Future Enhancements
- **Structured logging**: Winston hoặc Pino integration
- **Request tracing**: Correlation IDs
- **Performance monitoring**: APM integration (DataDog, New Relic)
- **Health checks**: /health endpoint implementation

## Security Considerations

### Current Security Measures
- **Input validation**: class-validator decorators
- **Type safety**: TypeScript compilation
- **Environment validation**: Joi schemas

### Recommended Security Enhancements
- **Helmet**: Security headers
- **CORS**: Cross-origin resource sharing configuration
- **Rate limiting**: Express rate limit middleware
- **Authentication**: JWT implementation
- **Authorization**: Role-based access control

## Performance Optimizations

### Current Optimizations
- **Connection pooling**: TypeORM default
- **Lazy loading**: Entity relationships
- **Indexing**: Database-level (manual implementation needed)

### Future Optimizations
- **Query optimization**: TypeORM query builder
- **Caching**: Redis integration
- **Compression**: Gzip middleware
- **CDN**: Static asset serving
