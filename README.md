# PathPoint API

A robust and secure authentication API built with Node.js, Express, TypeScript, and MongoDB.

## 🚀 Features

### 🔐 Authentication
- **Local Registration & Login** - Email/password based authentication
- **OAuth Integration** - Google & Facebook OAuth2 support
- **JWT Tokens** - Access tokens (15 mins) + Refresh tokens (7 days)
- **Cookie-based Auth** - HTTP-only, secure refresh token storage
- **Password Reset** - Secure email-based password recovery

### 🛡️ Security
- **Rate Limiting** - Global and authentication-specific limits
- **Input Validation** - Joi schema validation
- **Password Hashing** - bcrypt with configurable salt rounds
- **CORS Protection** - Configured for frontend integration
- **Security Headers** - Helmet.js for enhanced security
- **NoSQL Injection Protection** - Request body sanitization

### 📚 Documentation
- **Swagger UI** - Interactive API documentation
- **OpenAPI 3.0** - Comprehensive API specs
- **Examples** - Request/response examples for all endpoints

## 🛠️ Tech Stack

- **Runtime**: Node.js
- **Framework**: Express.js
- **Language**: TypeScript
- **Database**: MongoDB with Mongoose
- **Authentication**: Passport.js + JWT
- **Validation**: Joi
- **Documentation**: Swagger/OpenAPI
- **Security**: Helmet, CORS, Rate Limiting
- **Email**: Nodemailer with Gmail SMTP

## 📦 Installation

### Prerequisites
- Node.js (v18+)
- MongoDB (local or Atlas)
- Gmail account (for email features)

### Setup

1. **Clone the repository**
```bash
git clone <repository-url>
cd PathPoint
```

2. **Install dependencies**
```bash
npm install
```

3. **Environment Configuration**
```bash
cp .env.example .env
```

4. **Configure environment variables**
```env
# App
NODE_ENV=development
PORT=3000

# Database
MONGO_URI=mongodb://localhost:27017/pathpoint

# Client
CLIENT_URL=http://localhost:5173

# Google OAuth
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret
GOOGLE_CALLBACK_URL=http://localhost:3000/api/auth/google/callback

# Facebook OAuth
FACEBOOK_CLIENT_ID=your-facebook-client-id
FACEBOOK_CLIENT_SECRET=your-facebook-client-secret
FACEBOOK_CALLBACK_URL=http://localhost:3000/api/auth/facebook/callback

# JWT
JWT_SECRET=your-jwt-secret
REFRESH_TOKEN_SECRET=your-refresh-token-secret

# Email
EMAIL_USER=your-gmail@gmail.com
EMAIL_PASSWORD=your-gmail-app-password

# Security
BCRYPT_SALT_ROUNDS=12
```

### OAuth Setup

#### Google OAuth
1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create new project or select existing
3. Enable Google+ API
4. Create OAuth 2.0 credentials
5. Add redirect URI: `http://localhost:3000/api/auth/google/callback`

#### Facebook OAuth
1. Go to [Facebook Developers](https://developers.facebook.com/)
2. Create new app
3. Add Facebook Login product
4. Configure OAuth redirect URI: `http://localhost:3000/api/auth/facebook/callback`

#### Email Setup (Gmail)
1. Enable 2-Step Verification on your Gmail account
2. Generate App Password
3. Use App Password in `EMAIL_PASSWORD` environment variable

## 🚀 Running the Application

### Development
```bash
npm run dev
```

### Production
```bash
npm run build
npm start
```

### Health Check
```bash
curl http://localhost:3000/api/health
```

## 📚 API Documentation

### Swagger UI
Visit `http://localhost:3000/api-docs` for interactive API documentation.

### Authentication Endpoints

#### Local Auth
```http
POST /api/auth/register
POST /api/auth/login
POST /api/auth/refresh
```

#### OAuth
```http
GET /api/auth/google
GET /api/auth/facebook
GET /api/auth/google/callback
GET /api/auth/facebook/callback
```

#### Password Reset
```http
POST /api/auth/reset-password
POST /api/auth/verify-reset-password-code
POST /api/auth/update-password
```

### Request Examples

#### Register User
```bash
curl -X POST http://localhost:3000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Doe",
    "email": "john@example.com",
    "password": "password123"
  }'
```

#### Login User
```bash
curl -X POST http://localhost:3000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "john@example.com",
    "password": "password123"
  }'
```

#### Refresh Token
```bash
curl -X POST http://localhost:3000/api/auth/refresh \
  -H "Content-Type: application/json" \
  -d '{
    "refreshToken": "your-refresh-token"
  }'
```

## 🔧 Configuration

### JWT Configuration
- **Access Token**: 15 minutes expiration
- **Refresh Token**: 7 days expiration
- **Storage**: HTTP-only cookie for refresh token

### Rate Limiting
- **Global**: 100 requests per 15 minutes
- **Auth**: 20 requests per 15 minutes

### Security Features
- **Helmet.js**: Security headers
- **CORS**: Cross-origin resource sharing
- **HPP**: HTTP parameter pollution protection
- **Compression**: Response compression
- **Body Sanitization**: NoSQL injection protection

## 🗂️ Project Structure

```
src/
├── config/
│   ├── env.ts           # Environment validation
│   └── jwt.ts           # JWT configuration
├── docs/
│   ├── swagger.ts       # Swagger configuration
│   └── auth.apis.ts     # API documentation
├── middlewares/
│   ├── error.middleware.ts    # Error handling
│   ├── ratelimiter.ts         # Rate limiting
│   └── validate.ts            # Input validation
├── modules/auth/
│   ├── models/
│   │   ├── user.model.ts
│   │   ├── account.model.ts
│   │   └── forgetPassword.model.ts
│   ├── strategies/
│   │   ├── strategy.ts
│   │   └── passport.strategy.ts
│   ├── auth.controller.ts
│   ├── auth.service.ts
│   ├── auth.route.ts
│   ├── auth.validation.ts
│   └── auth.types.ts
├── services/
│   └── email.ts         # Email service
├── utils/
│   └── ApiError.ts      # Custom error class
├── app.ts               # Express app setup
└── server.ts            # Server startup
```

## 🧪 Testing

### Environment Setup
```bash
# Test environment
NODE_ENV=test
MONGO_URI=mongodb://localhost:27017/pathpoint-test
```

### Running Tests
```bash
npm test
```

## 🚀 Deployment

### Environment Variables for Production
```env
NODE_ENV=production
PORT=3000
CLIENT_URL=https://your-frontend-domain.com
GOOGLE_CALLBACK_URL=https://your-api-domain.com/api/auth/google/callback
FACEBOOK_CALLBACK_URL=https://your-api-domain.com/api/auth/facebook/callback
```

### Production Considerations
- Use HTTPS in production
- Set secure cookie flags
- Configure proper CORS origins
- Use environment-specific secrets
- Enable logging and monitoring
- Set up database backups

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## 📝 License

This project is licensed under the ISC License.

## 🆘 Support

For support and questions:
- Create an issue in the repository
- Check the API documentation at `/api-docs`
- Review the environment configuration

## 🔒 Security Notes

- Always use HTTPS in production
- Keep environment variables secure
- Regularly update dependencies
- Monitor security advisories
- Use strong secrets for JWT and OAuth
- Implement proper logging and monitoring

## 📊 Monitoring

### Health Endpoints
- `/api/health` - Basic health check
- Logs and metrics should be implemented for production

### Error Handling
- Structured error responses
- Development vs production error details
- Custom error classes for better debugging

---

**Built with ❤️ for secure authentication**
