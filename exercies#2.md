### **Exercise 2: Advanced Dockerfile for Python Application**

**Question:**

Create a Dockerfile for an advanced Python application with the following requirements:

1. The application should:
   - Use `python:3.10-slim` as the base image.
   - Install dependencies from a `requirements.txt` file.
   - Use a non-root user for running the application.
2. Set up environment variables for the application, including:
   - `APP_ENV` set to `production`
   - `APP_DEBUG` set to `false`
3. Optimize for a smaller image size by cleaning up unnecessary files after installation.
4. Expose port `8080` and run the application using `gunicorn`.
5. you need with commands to install dependencis in image: apt-get update && apt-get install -y \
    build-essential && \
    pip install --no-cache-dir -r requirements.txt && \
    apt-get purge -y build-essential && \
    apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/*
6. cmd for app is : ["gunicorn", "-w", "4", "-b", "0.0.0.0:8080", "app:app"]

**Application Files:**

`requirements.txt`
```
flask
gunicorn
```

`app.py`
```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "Advanced Docker Application"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8080)
```
