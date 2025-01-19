### **Exercise 1: Docker Compose for Redis, Flask, and PostgreSQL**

**Question:**

Create a `docker-compose.yml` file to set up the following services:

1. **Redis**: An in-memory data store.
2. **Flask**: A Python application that uses Redis and PostgreSQL.
3. **PostgreSQL**: A relational database with the following settings:
    - PostgreSQL user: `admin`
    - Password: `admin_pass`
    - Database name: `flask_db`

**Requirements:**
- create your own Dockerfile for python  app
- cmd for python app is "python app.py"
- install requirements.txt "pip install --no-cache-dir -r requirements.txt"
- Ensure PostgreSQL data is persistent.
- Expose the Flask application on port `5000`.
- All services must communicate on a custom Docker network named `flask_network`.
- use image: redis:alpine, image: postgres:alpine
- for postgres volumes: db_data:/var/lib/postgresql/data
- Attention app port is 5000
**Application Files:**

`flask_app/Dockerfile`
```dockerfile
FROM python:3.10-slim

WORKDIR /app

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["python", "app.py"]
```

`flask_app/requirements.txt`
```
flask
redis
psycopg2-binary
```

`flask_app/app.py`
```python
from flask import Flask
import redis
import psycopg2

app = Flask(__name__)

# Connect to Redis
redis_client = redis.StrictRedis(host='redis', port=6379, decode_responses=True)

# Connect to PostgreSQL
def connect_to_db():
    conn = psycopg2.connect(
        dbname="flask_db",
        user="admin",
        password="admin_pass",
        host="db"
    )
    return conn

@app.route('/')
def home():
    redis_client.set('message', 'Hello from Redis!')
    message = redis_client.get('message')
    return f"{message} \n Connected to PostgreSQL!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```
