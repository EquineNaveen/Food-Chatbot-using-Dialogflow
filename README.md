# Food Chatbot using Dialogflow

A conversational AI chatbot for food ordering built with **Google Dialogflow**, **FastAPI**, and **MySQL**. This project enables customers to place food orders, modify them, track order status, and interact with a restaurant's ordering system through natural language.

## 🚀 Features

- **Natural Language Ordering**: Place food orders using conversational AI
- **Order Management**: Add items to cart, remove items, and modify quantities
- **Order Completion**: Complete orders and receive order ID with total price
- **Order Tracking**: Track order status using order ID
- **Database Integration**: Persistent storage with MySQL database
- **Web Interface**: Simple frontend for restaurant information and menu
- **Docker Support**: Easy deployment with Docker and Docker Compose
- **Session Management**: Maintains order state across conversation sessions

## 🛠️ Technology Stack

- **Backend**: FastAPI (Python 3.11+)
- **AI/NLP**: Google Dialogflow
- **Database**: MySQL 8.0
- **Frontend**: HTML, CSS, JavaScript
- **Containerization**: Docker & Docker Compose
- **Package Management**: UV (Python package manager)

## 📋 Prerequisites

- Python 3.11 or higher
- Docker and Docker Compose
- Google Cloud Platform account (for Dialogflow)
- MySQL 8.0 (if running without Docker)

## 🏗️ Project Structure

```
Food-Chatbot-using-Dialogflow-1/
├── main.py                 # FastAPI application and webhook handlers
├── db_helper.py           # Database operations and MySQL connection
├── generic_helper.py      # Utility functions for session and string handling
├── pyproject.toml         # Python dependencies and project configuration
├── uv.lock               # UV lock file for dependency management
├── Dockerfile            # Docker container configuration
├── docker-compose.yml    # Multi-container application setup
├── ngrok.exe            # Tunneling tool for local development
├── db/
│   └── pandeyji_eatery.sql  # Database schema and initial data
└── frontend/
    ├── home.html         # Restaurant homepage
    ├── styles.css        # CSS styling
    ├── banner.jpg        # Banner image
    ├── menu1.jpg         # Menu images
    ├── menu2.jpg
    └── menu3.jpg
```

## ⚡ Quick Start

### Option 1: Using Docker Compose (Recommended)

1. **Clone the repository**
   ```bash
   git clone https://github.com/EquineNaveen/Food-Chatbot-using-Dialogflow.git
   cd Food-Chatbot-using-Dialogflow-1
   ```

2. **Start the application**
   ```bash
   docker-compose up --build
   ```

3. **Access the application**
   - API: http://localhost:8000
   - Frontend: http://localhost:8000/static/home.html
   - Database: localhost:3307

### Option 2: Local Development

1. **Install UV (if not already installed)**
   ```bash
   pip install uv
   ```

2. **Install dependencies**
   ```bash
   uv sync
   ```

3. **Set up MySQL database**
   - Install MySQL 8.0
   - Create database using `db/pandeyji_eatery.sql`
   - Update database credentials in `db_helper.py` if needed

4. **Run the application**
   ```bash
   uv run uvicorn main:app --host 0.0.0.0 --port 8000 --reload
   ```

## 🗃️ Database Schema

The application uses three main tables:

### `food_items`
- `item_id` (INT, Primary Key)
- `name` (VARCHAR)
- `price` (DECIMAL)

### `orders`
- `order_id` (INT, Primary Key)
- `item_id` (INT, Foreign Key)
- `quantity` (INT)
- `total_price` (DECIMAL)

### `order_tracking`
- `order_id` (INT, Primary Key)
- `status` (VARCHAR) - "in progress", "delivered", etc.

## 🤖 Dialogflow Integration

### Intents Handled

1. **order.add**: Add items to the current order
2. **order.remove**: Remove items from the current order
3. **order.complete**: Finalize and save the order to database
4. **track.order**: Track order status using order ID

### Webhook Configuration

Configure your Dialogflow webhook URL to point to:
```
https://your-domain.com/
```

For local development with ngrok:
```bash
ngrok http 8000
```



## 📡 API Endpoints

### `POST /`
**Webhook endpoint for Dialogflow**
- Receives and processes Dialogflow webhook requests
- Handles all conversation intents
- Returns JSON response for bot fulfillment

### `GET /`
**Health check endpoint**
- Returns server status

### `GET /static/{file_path}`
**Static file serving**
- Serves frontend files (HTML, CSS, images)

## 🍽️ Menu Items

The restaurant offers the following items:

| Item | Price |
|------|-------|
| Pav Bhaji | $6.00 |
| Chole Bhature | $7.00 |
| Pizza | $8.00 |
| Mango Lassi | $5.00 |
| Masala Dosa | $6.00 |
| Vegetable Biryani | $9.00 |
| Vada Pav | $4.00 |
| Rava Dosa | $7.00 |
| Samosa | $5.00 |

## 🔧 Configuration

### Environment Variables

- `MYSQL_HOST`: MySQL server hostname (default: localhost)
- `MYSQL_ROOT_PASSWORD`: MySQL root password (default: root)
- `MYSQL_DATABASE`: Database name (default: pandeyji_eatery)

### Database Configuration

Update database connection settings in `db_helper.py`:
```python
cnx = mysql.connector.connect(
    host=os.environ.get('MYSQL_HOST', 'localhost'),
    user="root",
    password="root",
    database="pandeyji_eatery"
)
```

## 🧪 Testing

Test the webhook endpoint manually:
```bash
curl -X POST http://localhost:8000/ \
  -H "Content-Type: application/json" \
  -d '{
    "queryResult": {
      "intent": {"displayName": "order.add"},
      "parameters": {
        "food-item": ["pizza"],
        "number": [2]
      },
      "outputContexts": [{
        "name": "projects/project-id/agent/sessions/session-id/contexts/context-name"
      }]
    }
  }'
```

## 🚀 Deployment

### Using Docker
```bash
docker build -t food-chatbot .
docker run -p 8000:8000 food-chatbot
```

### Production Deployment
1. Set up a production MySQL database
2. Configure environment variables
3. Deploy to cloud platform (AWS, GCP, Azure)
4. Update Dialogflow webhook URL
5. Set up SSL certificate for HTTPS

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-feature`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature/new-feature`)
5. Create a Pull Request

## 📄 License

This project is open source and available under the [MIT License](LICENSE).



## 🙏 Acknowledgments

- Google Dialogflow for natural language processing
- FastAPI for the robust web framework
- MySQL for reliable data storage
- Docker for containerization support


**Happy Coding! 🍕🤖**