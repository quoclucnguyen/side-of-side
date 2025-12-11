# Project Brief - Side of Side

## Tên Dự Án
Side of Side

## Mô Tả Ngắn Gọn
Một ứng dụng backend NestJS TypeScript với chức năng quản lý người dùng cơ bản, sử dụng PostgreSQL làm database và TypeORM làm ORM.

## Vị trí Git Repository
https://github.com/quoclucnguyen/side-of-side.git

## Version Hiện Tại
0.0.1

## Core Requirements (Yêu cầu cốt lõi)
1. **Backend API** với NestJS framework
2. **User Management System** - Quản lý người dùng đầy đủ
3. **Database Integration** - PostgreSQL với TypeORM
4. **API Documentation** - Swagger integration
5. **Validation** - Class-validator cho DTO validation
6. **Environment Configuration** - Multi-environment config với Joi validation

## Mục Tiêu Chính
- Xây dựng một backend API robust và scalable
- Implement authentication và authorization cho users
- Cung cấp API documentation đầy đủ
- Đảm bảo code quality và best practices
- Preparation cho production deployment

## Phạm Vi Dự Án
### MVP Features
- [x] User CRUD operations
- [x] Database setup with PostgreSQL
- [x] API Documentation với Swagger
- [x] Input validation
- [x] Environment configuration

### Future Features (Dựa trên phân tích)
- Authentication & Authorization
- Role-based access control
- Email verification
- Password reset functionality
- User profile management
- API rate limiting
- Logging và monitoring

## Technical Constraints
- TypeScript bắt buộc
- NestJS framework
- PostgreSQL database
- TypeORM cho database operations
- Swagger cho API documentation
- Jest cho testing

## Success Metrics
- API response time < 200ms
- 100% test coverage cho core functionality
- Zero security vulnerabilities
- Clean code với ESLint + Prettier
- Proper error handling và logging
