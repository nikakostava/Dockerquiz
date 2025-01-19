# Task: Create and Run a Dockerized Nginx Server

## Objective
The goal of this task is to help you understand how to create and configure a Dockerfile to containerize an Nginx web server. You will use the provided `index.html` and `nginx.conf` files and write a Dockerfile to serve the custom HTML on port 4000.

---

## Files Provided
1. **`index.html`** (HTML file):
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Success</title>
</head>
<body>
    <h1>Good job</h1>
</body>
</html>
```

2. **`nginx.conf`** (Nginx configuration file):
```nginx
worker_processes auto;

events {
    worker_connections 1024;
}

http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    server {
        listen 4000; # Listen on port 4000

        server_name _;

        location / {
            root   /usr/share/nginx/html;
            index  index.html;
        }

        error_page 404 /404.html;
        location = /404.html {
            internal;
        }
    }
}
```

---

## Your Task

1. **Create a Dockerfile**
   - Use the official `nginx:latest` image as the base image.
   - Remove the default Nginx configuration file (`/etc/nginx/conf.d/default.conf`).
   - Copy the provided `nginx.conf` file into the container at `/etc/nginx/nginx.conf`.
   - Copy the provided `index.html` file into the container at `/usr/share/nginx/html/index.html`.
   - Expose port `4000` from the container.
   - Set the default command to start Nginx in the foreground.
   ```

4. **Verify the Setup**
   - Open a web browser or use `curl` to navigate to `http://localhost:4000`.
   - Ensure the page displays:
     ```html
     <h1>Good job</h1>
     ```


