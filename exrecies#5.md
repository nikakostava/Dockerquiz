### **Exercise 5: Push Docker Image to Public DockerHub Registry**

**Question:**


1. Push the image to your public Docker Hub repository.
2. Image must be from exercies #4

**Requirements:**
- Replace `<username>` with your Docker Hub username.
- The image should be tagged as `<username>/python-app:latest` and '<username>/python-app:1.0.0'

**Answer:**

**Steps:**

1. Build the Docker image:
   ```bash
   docker build -t <username>/python-app:latest .
   ```

2. Log in to Docker Hub:
   ```bash
   docker login
   ```

3. Push the image:
   ```bash
   docker push <username>/python-app:latest
   ```

---
