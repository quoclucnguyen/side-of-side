# System Patterns - Side of Side

## Architecture Overview
Side of Side follows **Layered Architecture Pattern** với NestJS, implement separation of concerns và dependency injection.

```
┌─────────────────────────────────────┐
│           Controllers Layer          │ ← HTTP Request/Response Handling
├─────────────────────────────────────┤
│            Services Layer           │ ← Business Logic
├─────────────────────────────────────┤
│          Repositories Layer         │ ← Data Access Logic
├─────────────────────────────────────┤
│           Database Layer            │ ← PostgreSQL + TypeORM
└─────────────────────────────────────┘
```

## Key Technical Decisions

### 1. Modular Architecture
- **Pattern**: Feature-based modules
- **Rationale**: Better separation of concerns, easier testing và maintenance
- **Implementation**: Mỗi feature có module riêng (users, auth, etc.)

### 2. Dependency Injection
- **Pattern**: Constructor-based DI
- **Rationale**: Loose coupling, easier testing, better scalability
- **Implementation**: NestJS built-in DI container

### 3. Entity-Based Database Design
- **Pattern**: Active Record với TypeORM entities
- **Rationale**: Clean object-relational mapping, type safety
- **Implementation**: Decorator-based entities với relationships

## Component Relationships

### Core Flow Pattern
```
Request → Controller → Service → Repository → Database
   ↑                                                    ↓
Response ← DTO/Entity ← Business Logic ← Query/Result
```

### Module Dependencies
```
AppModule
├── ConfigModule (Global)
├── TypeOrmModule (Global)
├── UsersModule
│   ├── UsersController
│   ├── UsersService
│   └── UsersRepository (implicit via TypeORM)
└── [Future Modules]
    ├── AuthModule
    ├── RolesModule
    └── ProfilesModule
```

## Design Patterns in Use

### 1. Repository Pattern
- **Implementation**: TypeORM repositories
- **Benefits**: Abstraction layer, testability, separation of concerns
- **Location**: Service layer interacts với repositories

### 2. DTO Pattern
- **Implementation**: Class-validator decorated classes
- **Benefits**: Input validation, API documentation, type safety
- **Location**: `dto/` folders trong mỗi module

### 3. Service Layer Pattern
- **Implementation**: Business logic trong services
- **Benefits**: Reusability, testability, separation from HTTP concerns
- **Location**: `*.service.ts` files

### 4. Module Pattern
- **Implementation**: NestJS modules
- **Benefits**: Encapsulation, dependency management, clear boundaries
- **Location**: `*.module.ts` files

## Critical Implementation Paths

### User Creation Flow
```
POST /users → UsersController.createUser()
  ↓
Validate DTO (class-validator)
  ↓
UsersService.createUser()
  ↓
Check email uniqueness
  ↓
UserEntity.create()
  ↓
Repository.save()
  ↓
Return created user DTO
```

### Database Connection Flow
```
AppModule.init()
  ↓
ConfigModule loads environment
  ↓
TypeOrmModule.forRootAsync()
  ↓
Connect to PostgreSQL
  ↓
Auto-load entities
  ↓
Synchronize schema (dev mode)
```

## Configuration Patterns

### Environment Configuration
- **Pattern**: Hierarchical environment files
- **Priority**: `.env.development.local` → `.env.development` → `.env`
- **Validation**: Joi schema validation

### Database Configuration
- **Pattern**: Async factory with dependency injection
- **Benefits**: Environment-specific configs, testability
- **Features**: Auto-sync, logging, connection pooling

## Security Patterns

### Input Validation
- **Pattern**: Decorator-based validation
- **Implementation**: class-validator + class-transformer
- **Location**: DTO classes

### Entity Exposure Control
- **Pattern**: API property decorators
- **Implementation**: @ApiProperty() selective exposure
- **Benefits**: Control over API documentation và response data

## Error Handling Patterns

### Global Exception Filter (Future)
- **Pattern**: Centralized error handling
- **Implementation**: NestJS exception filters
- **Benefits**: Consistent error responses, logging

### Validation Error Pattern
- **Pattern**: Automatic 400 responses
- **Implementation**: ValidationPipe with transform
- **Benefits**: Automatic validation, type conversion

## Future Architecture Patterns

### CQRS Pattern (Planned)
- **Use Case**: Complex read/write operations
- **Implementation**: @nestjs/cqrs module
- **Benefits**: Scalability, separation of concerns

### Event-Driven Architecture (Planned)
- **Use Case**: Async operations, external integrations
- **Implementation**: Message queues, event emitters
- **Benefits**: Loose coupling, scalability

### Microservices Pattern (Considered)
- **Use Case**: Service splitting at scale
- **Implementation**: @nestjs/microservices
- **Benefits**: Independent deployment, technology diversity
