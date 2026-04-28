🚀 Laravel Dockerized Application

A containerized Laravel application using Nginx, PHP-FPM, and MySQL, with frontend assets built via Node.js.

📌 Overview

This project demonstrates a clean Docker-based Laravel setup with:

Nginx as web server
PHP-FPM (8.4) for application runtime
MySQL database
Node.js for frontend asset compilation
Docker Compose for orchestration
Utility containers for Composer and npm
🏗️ Tech Stack
Laravel
Nginx
PHP-FPM (8.4)
MySQL
Node.js + npm
Docker & Docker Compose


📂 Project Structure
.
├── docker-compose.yaml
├── dockerfiles/
│   └── php.dockerfile
├── nginx/
│   └── nginx.conf
├── src/                # Laravel application
└── env/
⚙️ Setup Instructions


1. Clone the repository
git clone <your-repo-url>
cd laravel-docker-project

2. Install Laravel (Composer utility container)
docker run --rm -v $(pwd)/src:/app composer create-project --prefer-dist laravel/laravel . 

3. Start containers
docker compose up -d --build 

4. Set required permissions
docker compose exec php sh -c "chown -R www-data:www-data /var/www/html/storage /var/www/html/bootstrap/cache /var/www/html/database && chmod -R 775 /var/www/html/storage /var/www/html/bootstrap/cache /var/www/html/database" 

5. Build frontend assets (npm)

Install dependencies:

docker run --rm -v $(pwd)/src:/app -w /app node:20-alpine npm install

Build assets:

docker run --rm -v $(pwd)/src:/app -w /app node:20-alpine npm run build

6. Access the application
http://localhost:8000
🧰 Utility Containers

This project uses ephemeral containers instead of defining tools in docker-compose.yaml.

Composer
docker run --rm -v $(pwd)/src:/app composer install

npm / Node.js
docker run --rm -v $(pwd)/src:/app -w /app node:20-alpine npm install
docker run --rm -v $(pwd)/src:/app -w /app node:20-alpine npm run build

Artisan
docker compose exec php php artisan migrate

🔄 Useful Commands

Start containers:

docker compose up -d

Stop containers:

docker compose down

Remove containers and volumes:

docker compose down -v

Rebuild containers:

docker compose up -d --build --force-recreate


🚀 Notes
Frontend assets are compiled into:
src/public/build

Laravel runs inside the PHP container and is served through Nginx
👨‍💻 Author

Built as part of a hands-on DevOps learning journey.