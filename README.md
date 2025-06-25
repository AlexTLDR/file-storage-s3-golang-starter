# Tubely

A powerful SaaS platform designed to help YouTubers efficiently manage their video assets, metadata, and content workflow.

## Overview

Tubely is a comprehensive video asset management system that streamlines the content creation process for YouTubers. The platform provides secure file storage, metadata management, and version control for video files and thumbnails, all built with scalability and performance in mind.

## Features

### Core Functionality
- **Video Upload & Storage**: Secure video file upload with S3 integration
- **Thumbnail Management**: Upload, store, and manage video thumbnails
- **Metadata Management**: Add and update video titles, descriptions, and custom metadata
- **Version Control**: Track and manage different versions of video assets
- **Asset Organization**: Organize videos and thumbnails with advanced categorization

### Technical Features
- **Cloud Storage**: AWS S3 integration for reliable file storage
- **CDN Distribution**: CloudFront integration for fast global content delivery
- **User Authentication**: JWT-based secure authentication system
- **Database Support**: Flexible database support (SQLite for development, PostgreSQL for production)
- **RESTful API**: Clean, well-documented API endpoints
- **File Caching**: Intelligent caching system for improved performance

## Tech Stack

- **Backend**: Go 1.23+
- **Database**: SQLite (development) / PostgreSQL (production)
- **Storage**: AWS S3
- **CDN**: AWS CloudFront
- **Authentication**: JWT tokens
- **Dependencies**:
  - `github.com/golang-jwt/jwt/v5` - JWT authentication
  - `github.com/lib/pq` - PostgreSQL driver
  - `github.com/mattn/go-sqlite3` - SQLite driver
  - `github.com/joho/godotenv` - Environment configuration
  - `github.com/google/uuid` - UUID generation

## Quick Start

### Prerequisites

- Go 1.23 or later
- AWS account with S3 bucket configured
- PostgreSQL (for production) or SQLite (for development)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-org/tubely.git
   cd tubely
   ```

2. **Install dependencies**
   ```bash
   go mod download
   ```

3. **Set up environment variables**
   ```bash
   cp .env.example .env
   # Edit .env with your configuration
   ```

4. **Configure your environment**
   ```env
   JWT_SECRET=your-super-secret-jwt-key
   PLATFORM=dev
   FILEPATH_ROOT=./uploads
   ASSETS_ROOT=./assets
   S3_BUCKET=your-s3-bucket-name
   S3_REGION=your-aws-region
   S3_CF_DISTRIBUTION=your-cloudfront-distribution-id
   PORT=8080
   DATABASE_URL=your-database-connection-string
   ```

5. **Run the application**
   ```bash
   go run main.go
   ```

The server will start on `http://localhost:8080` (or your configured port).

## API Endpoints

### Authentication
- `POST /api/login` - User login
- `POST /api/refresh` - Refresh JWT token

### User Management
- `GET /api/users` - Get user information
- `POST /api/users` - Create new user

### Video Management
- `POST /api/videos/upload` - Upload video file
- `GET /api/videos/{id}/metadata` - Get video metadata
- `PUT /api/videos/{id}/metadata` - Update video metadata

### Thumbnail Management
- `POST /api/thumbnails/upload` - Upload thumbnail
- `GET /api/thumbnails/{id}` - Get thumbnail

## Configuration

### Environment Variables

| Variable | Description | Default | Required |
|----------|-------------|---------|----------|
| `JWT_SECRET` | Secret key for JWT token generation | - | Yes |
| `PLATFORM` | Platform environment (dev/prod) | dev | No |
| `FILEPATH_ROOT` | Root directory for file storage | ./uploads | No |
| `ASSETS_ROOT` | Root directory for static assets | ./assets | No |
| `S3_BUCKET` | AWS S3 bucket name | - | Yes |
| `S3_REGION` | AWS S3 region | - | Yes |
| `S3_CF_DISTRIBUTION` | CloudFront distribution ID | - | No |
| `PORT` | Server port | 8080 | No |
| `DATABASE_URL` | Database connection string | - | Yes |

### AWS Configuration

Ensure your AWS credentials are configured via:
- AWS credentials file (`~/.aws/credentials`)
- Environment variables (`AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`)
- IAM roles (for EC2/ECS deployment)

Required S3 permissions:
- `s3:GetObject`
- `s3:PutObject`
- `s3:DeleteObject`

## Development

### Running Tests
```bash
go test ./...
```

### Database Migrations
```bash
# Run migrations
go run ./cmd/migrate

# Reset database (development only)
go run reset.go
```

### Sample Data
```bash
# Download sample files
./samplesdownload.sh
```

## Project Structure

```
.
├── main.go                 # Application entry point
├── handler_*.go           # HTTP request handlers
├── assets.go              # Static asset handling
├── cache.go               # Caching utilities
├── json.go                # JSON utilities
├── reset.go               # Database reset utility
├── internal/
│   └── database/          # Database models and queries
├── app/                   # Application configuration
├── assets/                # Static assets
└── samples/               # Sample files
```

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Guidelines

- Follow Go best practices and conventions
- Write comprehensive tests for new features
- Update documentation for API changes
- Use meaningful commit messages
- Ensure all tests pass before submitting PR

## Deployment

### Production Deployment

1. Set up production environment variables
2. Configure PostgreSQL database
3. Set up AWS S3 and CloudFront
4. Build the application:
   ```bash
   go build -o tubely
   ```
5. Deploy to your preferred platform (AWS ECS, Google Cloud Run, etc.)

## Security

- All file uploads are validated and sanitized
- JWT tokens expire and require refresh
- S3 bucket policies should follow least-privilege principle
- Use HTTPS in production
- Regular security audits recommended

## Support

For support, please open an issue on GitHub or contact our support team.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Roadmap

- [ ] Advanced video analytics
- [ ] Bulk upload capabilities
- [ ] Integration with YouTube API
- [ ] Advanced search and filtering
- [ ] Team collaboration features
- [ ] Mobile app support

---
