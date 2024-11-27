# Test Nginx, MySQL, and phpMyAdmin Docker Setup

This repository provides a simple Docker Compose setup to run an Nginx server, MySQL database, and phpMyAdmin interface using local Docker images. It is designed for testing and development purposes.

## Features
- **Nginx**: Lightweight web server using the `nginx:alpine` image.
- **MySQL**: Database server using the `mysql:8.0` image.
- **phpMyAdmin**: Web-based interface for managing MySQL databases using the `phpmyadmin:latest` image.

## Prerequisites
- Docker installed on your system.
- Docker Compose installed.

## Getting Started

### Clone the Repository
```
git clone https://github.com/yourusername/test-nginx-MySQL-phpMyAdmin.git
cd test-nginx-MySQL-phpMyAdmin
```

### Project Structure
```
test-nginx-MySQL-phpMyAdmin/
├── docker-compose.yml
├── nginx.conf
└── README.md
```

- **docker-compose.yml**: Defines the services for Docker Compose.
- **nginx.conf**: Nginx configuration file.
- **README.md**: Documentation.

### How to Run

1. **Start the Containers**:
   Run the following command to start all services:
   ```
   docker-compose up -d
   ```

2. **Verify the Services**:
   - Nginx: [http://localhost](http://localhost)
   - phpMyAdmin: [http://localhost:8080](http://localhost:8080)

3. **Stop the Containers**:
   ```
   docker-compose down
   ```

### Configuration Details

#### MySQL
- **Image**: `mysql:8.0`
- **Container Name**: `test-mysql`
- **Environment Variables**:
  - `MYSQL_ROOT_PASSWORD`: `rootpassword`
  - `MYSQL_DATABASE`: `testdb`
  - `MYSQL_USER`: `testuser`
  - `MYSQL_PASSWORD`: `testpassword`
- **Ports**: `3306:3306`
- **Volume**: Persists data in the `mysql_data` volume.

#### phpMyAdmin
- **Image**: `phpmyadmin:latest`
- **Container Name**: `test-phpmyadmin`
- **Environment Variables**:
  - `PMA_HOST`: `mysql`
  - `PMA_USER`: `root`
  - `PMA_PASSWORD`: `rootpassword`
- **Ports**: `8080:80`

#### Nginx
- **Image**: `nginx:alpine`
- **Container Name**: `test-nginx`
- **Ports**: `80:80`
- **Volume**: Maps `nginx.conf` for server configuration.

### File `nginx.conf`
```
events { }

http {
    server {
        listen 80;
        location / {
            root /usr/share/nginx/html;
            index index.html;
        }
    }
}
```

### Volume Management
The MySQL data is stored in a Docker volume named `mysql_data`. To remove the data volume:
```
docker volume rm test-nginx-MySQL-phpMyAdmin_mysql_data
```

## Troubleshooting

1. **Check Logs**:
   Use the following command to view logs for a specific service:
   ```bash
   docker-compose logs <service_name>
   ```

2. **Common Issues**:
   - **Port Conflicts**: Ensure that ports `80` and `8080` are not in use by other services.
   - **Connection Errors in phpMyAdmin**: Verify that the `PMA_HOST` and credentials match the MySQL service configuration.

## License
This project is open-source and available under the [MIT License](LICENSE).

## Contributing
Contributions are welcome! Feel free to open an issue or submit a pull request.

## Contact
For questions or support, please contact [wira](mailto:mwiraadekusuma@duck.com).
