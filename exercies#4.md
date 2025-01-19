### **Exercise 4: Multi-Stage Docker Image Build**

**Question:**

Write a Dockerfile for a Python application that:

1. Uses a multi-stage build to optimize the image size.
2. The application should:
   - Use `python:3.10-slim` as the base image in the final stage.
   - Install dependencies from a `requirements.txt` file in the first stage.
   - Copy the application code from the current directory.
3. Run the application using `python app.py`.

**Application Files:**

`requirements.txt`
```
flask
```

`app.py`
```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "Hello, Docker!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

---
