# Student-Collaboration-Hub---Backend

A FastAPI-based backend application for a social community platform with user authentication, posts, comments, and replies functionality.

## 🌟 Features

- **User Management**: User registration, authentication, and profile management
- **Posts**: Create, read, and manage posts with categories, tags, and attachments
- **Comments & Replies**: Add comments to posts with threaded reply functionality
- **Likes & Saves**: Users can like and save posts
- **Authentication**: Secure user authentication using JWT tokens with password hashing
- **CORS Support**: Configured for frontend-backend communication
- **Database**: MongoDB integration for data persistence

## 🛠 Tech Stack

- **Framework**: [FastAPI](https://fastapi.tiangolo.com/) - Modern Python web framework
- **Server**: Uvicorn - ASGI server
- **Database**: MongoDB with [Motor](https://github.com/mongodb-motor/motor) (async driver)
- **Authentication**: JWT (python-jose) with bcrypt password hashing
- **Validation**: Pydantic for data validation
- **Environment**: python-dotenv for configuration management

## 📦 Dependencies

```
fastapi
uvicorn
motor
pydantic
pydantic[email]
passlib[bcrypt]
python-jose
python-multipart
python-dotenv
```

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- MongoDB instance running (local or cloud)
- pip package manager

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/neeru-meda/sch-backend.git
   cd sch-backend
   ```

2. **Create a virtual environment** (optional but recommended)
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure environment variables**
   ```bash
   cp .env.example .env
   ```
   Edit `.env` with your configuration:
   ```env
   FRONTEND_ORIGIN=http://localhost:3000
   DATABASE_URL=mongodb://localhost:27017
   SECRET_KEY=your-secret-key-here
   ```

5. **Run the application**
   ```bash
   uvicorn main:app --reload
   ```

   The API will be available at `http://localhost:8000`

## 📚 API Endpoints

### Health Check
- `GET /` - Check if backend is running

### Database
- `GET /db-test` - List all MongoDB collections

### Authentication
- `POST /auth/register` - Register a new user
- `POST /auth/login` - Login user
- `POST /auth/logout` - Logout user

### Users
- `GET /users/{user_id}` - Get user profile
- `PUT /users/{user_id}` - Update user profile

### Posts
- `GET /posts` - List all posts
- `POST /posts` - Create a new post
- `GET /posts/{post_id}` - Get a specific post
- `PUT /posts/{post_id}` - Update a post
- `DELETE /posts/{post_id}` - Delete a post
- `POST /posts/{post_id}/like` - Like a post
- `POST /posts/{post_id}/save` - Save a post

### Comments
- `GET /posts/{post_id}/comments` - Get comments for a post
- `POST /posts/{post_id}/comments` - Add a comment
- `PUT /comments/{comment_id}` - Update a comment
- `DELETE /comments/{comment_id}` - Delete a comment

### Replies
- `POST /comments/{comment_id}/replies` - Add a reply to a comment
- `PUT /replies/{reply_id}` - Update a reply
- `DELETE /replies/{reply_id}` - Delete a reply

## 📁 Project Structure

```
sch-backend/
├── main.py              # FastAPI application entry point
├── models.py            # Pydantic models for data validation
├── database.py          # MongoDB connection and configuration
├── requirements.txt     # Python dependencies
├── .env                 # Environment variables (not tracked in git)
├── seed_mock_data.py    # Script to seed sample data
└── routers/             # API route handlers
    ├── auth.py          # Authentication endpoints
    ├── user.py          # User management endpoints
    ├── post.py          # Post management endpoints
    └── comment.py       # Comment management endpoints
```

## 🔐 Data Models

### User
```python
{
    "_id": str,
    "username": str,
    "email": str,
    "password": str (hashed),
    "full_name": Optional[str],
    "bio": Optional[str],
    "department": Optional[str],
    "linkedin": Optional[str],
    "github": Optional[str],
    "college": Optional[str],
    "joined": datetime
}
```

### Post
```python
{
    "_id": str,
    "title": str,
    "content": str,
    "category": str,
    "link": Optional[str],
    "attachments": List[str],
    "tags": List[dict],
    "author": dict,
    "createdAt": datetime,
    "likes": List[str] (user IDs),
    "saves": List[str] (user IDs),
    "commentsCount": int
}
```

### Comment
```python
{
    "_id": str,
    "content": str,
    "author": dict,
    "createdAt": datetime,
    "likes": List[str],
    "replies": List[Reply],
    "post_id": str
}
```

## 🔌 Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `FRONTEND_ORIGIN` | Frontend URL for CORS | http://localhost:3000 |
| `DATABASE_URL` | MongoDB connection string | mongodb://localhost:27017 |
| `SECRET_KEY` | JWT secret key | (required) |
| `ALGORITHM` | JWT algorithm | HS256 |
| `ACCESS_TOKEN_EXPIRE_MINUTES` | Token expiration time | 30 |

## 📖 Documentation

Once the application is running, interactive API documentation is available at:
- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc

## 🗄️ Database Setup

### MongoDB Connection

Update your `.env` file with your MongoDB connection string:

```env
DATABASE_URL=mongodb://username:password@host:port/database_name
```

### Seeding Sample Data

Run the seed script to populate the database with sample data:

```bash
python seed_mock_data.py
```

## 🧪 Testing

To test the API endpoints, use the Swagger UI at `/docs` or make requests using tools like:
- cURL
- Postman
- HTTPie

Example request:
```bash
curl -X POST "http://localhost:8000/auth/register" \
  -H "Content-Type: application/json" \
  -d '{"username":"testuser","email":"test@example.com","password":"securepass123"}'
```

## 🔄 CORS Configuration

CORS is configured to allow requests from the frontend origin specified in the `.env` file. To allow multiple origins or modify settings, edit the `main.py` file.

## 👤 Author

[neeru-meda](https://github.com/neeru-meda)

---

**Created**: July 2025
