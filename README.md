# MagicVilla API

A modern and scalable RESTful Web API for villa management system. Built with .NET 7.0, this API provides full CRUD (Create, Read, Update, Delete) operations and JSON Patch support for managing villa information.

## ✨ Features

- **RESTful API**: Villa management using standard HTTP methods
- **CRUD Operations**: Create, read, update, and delete villas
- **JSON Patch Support**: Partial update operations using JSON Patch
- **Swagger/OpenAPI**: Automatic API documentation
- **Entity Framework Core**: Database management using Code-First approach
- **SQL Server Support**: Microsoft SQL Server database integration
- **Multiple Format Support**: Response support in JSON and XML formats
- **Serilog Integration**: Advanced logging support (optional)

## 🛠 Technologies

- **.NET 7.0**: Main framework
- **ASP.NET Core Web API**: Web API framework
- **Entity Framework Core 7.0**: ORM
- **SQL Server**: Database
- **Swashbuckle (Swagger)**: API documentation
- **Serilog**: Logging library
- **Newtonsoft.Json**: JSON operations and JSON Patch support

## 📦 Prerequisites

- [.NET 7.0 SDK](https://dotnet.microsoft.com/download/dotnet/7.0) or higher
- [SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads) (Express, Developer, or Enterprise)
- [Visual Studio 2022](https://visualstudio.microsoft.com/) or [Visual Studio Code](https://code.visualstudio.com/) (recommended)
- SQL Server Management Studio (SSMS) or Azure Data Studio (optional)

## 🚀 Installation

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd MagicVilla_API
   ```

2. **Create the database:**
   - Ensure your SQL Server is running
   - Update the connection string in `appsettings.json` according to your SQL Server settings

3. **Run database migrations:**
   ```bash
   cd MagicVilla_VillaAPI
   dotnet ef database update
   ```

4. **Run the project:**
   ```bash
   dotnet run
   ```

5. **Access Swagger UI:**
   - Navigate to `https://localhost:5001/swagger` or `http://localhost:5000/swagger` in your browser
   - Port number may vary based on settings in `launchSettings.json`


## 📡 API Endpoints

Base URL: `https://localhost:5001/api/VillaAPI` or `http://localhost:5000/api/VillaAPI`

### Get All Villas
```http
GET /api/VillaAPI
```
Returns a list of all villas.

**Response:** `200 OK` - List of villas

### Get Villa by ID
```http
GET /api/VillaAPI/{id}
```
Retrieves details of a specific villa.

**Parameters:**
- `id` (int): Villa ID

**Responses:**
- `200 OK` - Villa found
- `400 Bad Request` - Invalid ID
- `404 Not Found` - Villa not found

### Create New Villa
```http
POST /api/VillaAPI
Content-Type: application/json
```
Creates a new villa.

**Request Body:**
```json
{
  "name": "Villa Name",
  "details": "Villa details",
  "sqft": 2500,
  "rate": 500.00,
  "occupancy": 4,
  "imageUrl": "https://example.com/image.jpg",
  "amenity": "WiFi, Pool, Garage"
}
```

**Responses:**
- `201 Created` - Villa successfully created
- `400 Bad Request` - Invalid data or villa already exists

### Update Villa
```http
PUT /api/VillaAPI/{id}
Content-Type: application/json
```
Updates an existing villa completely.

**Parameters:**
- `id` (int): Villa ID

**Request Body:** VillaDTO object (all fields required)

**Responses:**
- `204 No Content` - Update successful
- `400 Bad Request` - Invalid data

### Partial Update Villa (JSON Patch)
```http
PATCH /api/VillaAPI/{id}
Content-Type: application/json-patch+json
```
Updates specific fields of a villa.

**Parameters:**
- `id` (int): Villa ID

**Request Body:**
```json
[
  {
    "op": "replace",
    "path": "/name",
    "value": "New Villa Name"
  },
  {
    "op": "replace",
    "path": "/rate",
    "value": 600.00
  }
]
```

**Responses:**
- `204 No Content` - Update successful
- `400 Bad Request` - Invalid data

### Delete Villa
```http
DELETE /api/VillaAPI/{id}
```
Deletes a villa.

**Parameters:**
- `id` (int): Villa ID

**Responses:**
- `204 No Content` - Deletion successful
- `400 Bad Request` - Invalid ID
- `404 Not Found` - Villa not found

## 📁 Project Structure

```
MagicVilla_API/
│
├── MagicVilla_VillaAPI/          # Main project folder
│   ├── Controllers/               # API Controllers
│   │   └── VillaAPIController.cs  # Villa API endpoints
│   ├── Data/                      # Database context
│   │   └── ApplicationDbContext.cs
│   ├── Models/                    # Data models
│   │   ├── Villa.cs              # Villa entity model
│   │   └── Dto/
│   │       └── VillaDTO.cs       # Villa Data Transfer Object
│   ├── Migrations/                # Entity Framework migrations
│   ├── Properties/                # Project properties
│   ├── appsettings.json          # Application settings
│   ├── appsettings.Development.json
│   └── Program.cs                # Application entry point
│
└── README.md                      # Project documentation
```

## 💻 Usage

### Testing with Swagger UI

1. After running the application, navigate to Swagger UI
2. Select the desired endpoint
3. Click "Try it out" button
4. Enter required parameters
5. Click "Execute" button