# Go RESTfulAPI Management

A RESTful API management built with Go, Gin, and GORM.

## Features

- **CRUD Operations**: Complete Create, Read, Update, Delete operations for products
- **Database Integration**: SQLite database with GORM ORM
- **API Documentation**: Swagger/OpenAPI documentation
- **Middleware**: Logging, CORS, Rate limiting, Security headers
- **Validation**: Request validation with custom error messages
- **Testing**: Unit tests for controllers
- **Environment Configuration**: Configurable via environment variables

## Tech Stack

- **Go 1.21+**
- **Gin Web Framework**
- **GORM** (with SQLite driver)
- **Swagger** (API documentation)
- **Testify** (testing framework)

## Project Structure

```
API-RentCar/
├── cmd/api/           # Application entry point
├── config/            # Configuration management
├── controllers/       # HTTP handlers
├── docs/              # Swagger documentation
├── middleware/        # HTTP middleware
├── models/            # Database models
├── routes/            # Route definitions
├── tests/             # Unit tests
├── utils/             # Utility functions
├── .env               # Environment variables
└── go.mod             # Go module file
```

## Getting Started

### Prerequisites

- Go 1.21 or higher
- Git

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd API-RentCar
```

2. Install dependencies:
```bash
go mod tidy
```

3. Copy and configure environment variables:
```bash
cp .env.example .env
```

4. Run the application:
```bash
go run cmd/api/main.go
```

5. Access the API documentation:
```
http://localhost:8080/swagger/index.html
```

6. Generate Swagger documentation:
```bash
go run github.com/swaggo/swag/cmd/swag@latest init -g cmd/api/main.go -o docs --parseDependency --parseInternal
```

7. Access points:
   - API endpoint: `http://localhost:8080`
   - API documentation: `http://localhost:8080/swagger/index.html`

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `PORT` | Server port | `8080` |
| `GIN_MODE` | Gin mode (debug/release) | `debug` |
| `DB_TYPE` | Database type | `sqlite` |
| `DB_PATH` | Database file path | `./rentcar.db` |
| `API_VERSION` | API version | `v1` |
| `API_TITLE` | API title | `RentCar API` |
| `API_DESCRIPTION` | API description | `Car Rental Management API` |

## API Endpoints

### Health Check
- `GET /health` - Health check endpoint

### Products
- `GET /api/v1/products` - Get all products (with pagination)
- `GET /api/v1/products/:id` - Get product by ID
- `POST /api/v1/products` - Create new product
- `PUT /api/v1/products/:id` - Update product
- `DELETE /api/v1/products/:id` - Delete product

### Documentation
- `GET /swagger/*` - Swagger UI documentation

## API Documentation

Once the server is running, you can access the interactive API documentation at:
`http://localhost:8080/swagger/index.html`

## Request/Response Examples

### Create Product
```bash
curl -X POST http://localhost:8080/api/v1/products \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Toyota Camry",
    "description": "Reliable sedan for city driving",
    "price_per_day": 45.99,
    "category": "Sedan",
    "available": true
  }'
```

### Get All Products
```bash
curl http://localhost:8080/api/v1/products?page=1&limit=10
```

### Get Product by ID
```bash
curl http://localhost:8080/api/v1/products/1
```

### Update Product
```bash
curl -X PUT http://localhost:8080/api/v1/products/1 \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Toyota Camry 2024",
    "price_per_day": 49.99
  }'
```

### Delete Product
```bash
curl -X DELETE http://localhost:8080/api/v1/products/1
```

## Testing

Run the test suite:
```bash
go test ./tests/...
```

Run tests with coverage:
```bash
go test -cover ./tests/...
```

## Development

### Adding New Endpoints

1. Define the model in `models/`
2. Create controller in `controllers/`
3. Add routes in `routes/routes.go`
4. Add Swagger annotations
5. Write tests in `tests/`

### Database Migrations

The application uses GORM's auto-migration feature. Models are automatically migrated on startup.

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests
5. Submit a pull request

## License

This project is licensed under the MIT License.