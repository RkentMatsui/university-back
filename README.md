# Laravel Docker Setup
This guide provides instructions for setting up a Laravel project with Docker using Nginx and MySQL. Follow these steps to get your development environment up and running.

## Prerequisites
- Docker
- Docker Compose

## Directory Structure
Ensure your project has the following structure:


```arduino
.
├── .setup
│   ├── Dockerfile
│   ├── docker-compose.yml
│   └── nginx
│       └── conf.d
│           └── laravel.conf
├── app
└──  ...
```

1. Clone the Repository
Clone this repository to your local machine:

```
git clone <repository-url>
cd <repository-directory>
```
2. Setup Docker Containers
Navigate to the .setup directory:

```
cd .setup
```
Build and start the Docker containers:

```
docker-compose up --build
```
This command will:

Build the Docker images.
Start the Nginx, PHP-FPM, and MySQL containers.
3. Configure Laravel
Create a Laravel Encryption Key

Once the containers are up, you need to generate a Laravel application key. Run the following command in the laravel_app container:


```
php artisan key:generate
```
This command will generate a new key and update your .env file automatically.

Run Migrations

To set up the database schema, run the migrations:


```
php artisan migrate
```
This will create the necessary tables in the database.

4. Access the Application
Once the setup is complete, you can access the Laravel application at:


```
http://localhost:8080
```
5. Troubleshooting
If you encounter issues, here are some common checks:

Database Connection Error:

Ensure that the database credentials in your .env file match those defined in docker-compose.yml.
Check if the MySQL container is running: docker-compose ps.
Verify the MySQL service logs: docker-compose logs db.
Nginx Configuration Error:

Ensure the Nginx configuration file (.setup/nginx/conf.d/laravel.conf) is correctly mapped and contains valid settings.
Check the Nginx container logs: docker-compose logs nginx.
Permissions Issues:

Ensure proper permissions for Laravel’s storage and bootstrap/cache directories:
```
docker-compose exec app chown -R www-data:www-data /var/www
docker-compose exec app chmod -R 755 /var/www/storage /var/www/bootstrap/cache
```
6. Stopping and Restarting Containers
To stop the containers, use:


```
docker-compose down
```
To restart the containers, use:


```
docker-compose up
```
7. Additional Notes
Docker Volumes: Ensure that your volumes are correctly mapped to avoid issues with file synchronization.
Configuration Files: If you make changes to .env or Docker configuration files, you may need to rebuild the Docker images using docker-compose build.


# To Push new version of the Docker Image to Github Packages
