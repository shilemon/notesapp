# Simple Notes App
This is a simple notes app built with React and Django.

## Requirements
1. Python 
2. Node.js
3. React

## Installation
1. Clone the repository
```
git clone https://github.com/Hitstar53/notesapp.git
```
2. Create a virtual environment and activate it
```
virtualenv venv
venv/bin/activate
```
3. Install the requirements
```
pip install -r requirements.txt
```
4. Run the server
```
python manage.py runserver
```

## Frontend - React
5. Open another terminal and navigate to the mynotes directory
```
cd mynotes
```
6. Install the dependencies
```
npm install
```
7. Run the app





# 🗒️ NotesApp - Dockerized Django with Nginx

This project is a simple Django application containerized with Docker and served via Nginx. It demonstrates how to use Docker Compose to orchestrate both a Django app and an Nginx reverse proxy.

---

## 📁 Project Structure

```
.
├── Dockerfile               # Builds the Django app container
├── docker-compose.yml       # Defines the multi-container setup
├── nginx.conf               # Nginx reverse proxy configuration
├── requirements.txt         # Python dependencies
├── db.sqlite3               # SQLite database (for dev use)
├── manage.py                # Django management script
└── notesapp/                # Your Django project directory
```

---

## ⚙️ How It Works

### Services

- **web**: Django app running on port `8000`
- **nginx**: Nginx reverse proxy forwarding traffic from port `8080` to the Django app

---

## 🧪 Running the Project using Docker ,docker-compose.yml file and Nginx.conf


### 📦 2. Build and start the services

```bash
docker-compose up --build
```

### 🌐 3. Access the application

Open your browser and visit:  
**http://localhost:8080**

---

## 🧱 Docker Configuration

### 🐳 Dockerfile

```dockerfile
FROM python:3.9

WORKDIR /app

COPY requirements.txt /app/
RUN pip install -r requirements.txt

COPY . /app

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
```

### 🧩 docker-compose.yml

```yaml
services:
  web:
    build: .
    container_name: django-app
    expose:
      - "8000"

  nginx:
    image: nginx:alpine
    ports:
      - "8080:80"
    volumes:
      - ./nginx.conf:/etc/nginx/conf.d/default.conf
    depends_on:
      - web
```

### 🌐 nginx.conf

```nginx
server {
    listen 80;

    location / {
        proxy_pass http://web:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

---

## 📝 Notes

- Make sure `nginx.conf` is in the root directory and correctly mapped in `docker-compose.yml`.
- You can change the Nginx port from `8080` to anything you like (just update `docker-compose.yml`).
- Don't forget to migrate and create a superuser if needed:

```bash
docker exec -it django-app python manage.py migrate
docker exec -it django-app python manage.py createsuperuser
```

---

## 📜 License

This project is for educational/demo purposes. Modify and use it freely.


<img width="1913" height="963" alt="image" src="https://github.com/user-attachments/assets/0275aa61-d045-43cf-ac45-93548fd8198b" />


```
npm start
```

## Deployment
App is deployed on Railway: [Notes App](https://notesapp-production-8c87.up.railway.app/)  
Refer this article on how to: [deploy a django app on Railway](https://dev.to/osahenru/using-railway-app-to-deploy-your-django-project-3ah1)
