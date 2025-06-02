# map-egypt-docker
To support docker deployment for map-egypt services.

## Developer Guide

### Prerequisites

- [Docker](https://docs.docker.com/get-docker/) (version 19.03.0+)
- [Docker Compose](https://docs.docker.com/compose/install/) (version 1.27.0+)

### Project Structure

The project consists of four main services:

1. **Database (PostgreSQL)**: Stores application data
2. **Site**: Frontend web application
3. **API**: Backend API service
4. **Admin**: Administration interface

### Volume Configuration

This project uses two persistent volumes:

- `pgdata`: Stores PostgreSQL database files
- `uploaded`: Stores files uploaded through the API

### Running the Application

#### 1. Clone the Repository

```bash
git clone https://github.com/cartologic/map-egypt-docker.git
cd map-egypt-docker
```

#### 2. Environment Configuration

Make sure the API environment file exists:

```bash
# Verify that the .env file exists in the api directory
ls -la ./api/.env
```

If the file doesn't exist, create it with the necessary environment variables.

#### 3. Start the Services

```bash
docker-compose up -d
```

This command builds and starts all services in detached mode. The first run will take longer as it needs to build the images.

#### 4. Verify Services

Check if all services are running properly:

```bash
docker-compose ps
```

#### 5. Access the Applications

- **Site**: [http://localhost:9023](http://localhost:9023)
- **Admin Interface**: [http://localhost:9021](http://localhost:9021)
- **API**: [http://localhost:9011](http://localhost:9011)
- **Database**: Available on port 9044 (connect using a PostgreSQL client)

### Managing Data Volumes

#### Volume Locations

- PostgreSQL data: `./pgdata` (mapped to `/var/lib/postgresql/data` in the container)
- Uploaded files: `./uploaded` (mapped to `/app/uploaded` in the API container)


### Stopping the Application

```bash
# Stop the services but keep the volumes
docker-compose down

# Stop the services and remove the volumes (CAUTION: This will delete all data)
docker-compose down -v
```

### Troubleshooting

#### Viewing Logs

```bash
# View logs for all services
docker-compose logs

# View logs for a specific service
docker-compose logs [service_name]

# Follow logs in real-time
docker-compose logs -f [service_name]
```

#### Restarting Services

```bash
# Restart a specific service
docker-compose restart [service_name]

# Restart all services
docker-compose restart
```

#### Rebuilding Services

If you've made changes to the source code and need to rebuild:

```bash
docker-compose build [service_name]
docker-compose up -d [service_name]
```
