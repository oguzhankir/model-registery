### Commands

To run the project, use the following commands:

1. **Remove all unused containers, networks, images (both dangling and unreferenced), and optionally, volumes:**
    ```bash
    sudo docker system prune -a --volumes
    ```

2. **Build and start the Docker container:**
    ```bash
    sudo docker-compose up --build
    ```

## Project Structure

### Root Directory

- **`.gitignore`**: Specifies files and directories to be ignored by Git.
- **`customer_purchases.csv`**: CSV file containing customer purchase data.
- **`docker-compose.yml`**: Docker Compose configuration file for defining and running multi-container Docker applications.
- **`Dockerfile`**: Dockerfile for building the Docker image of the application.
- **`main.py`**: Entry point for the application.
- **`nginx.conf`**: Configuration file for Nginx.
- **`README.md`**: Bu dosya case açıklamasını içeriyor..
- **`requirements.txt`**: Lists the Python packages required for the project.
- **`settings.toml`**: Configuration file in TOML format for application settings.

### `README` Directory

- **`SOLUTION_OVERVIEW.md`**: Provides an overview of the solution.
- **`SWAGGER_DOCUMENTATION.md`**: Contains the Swagger API documentation for the service, detailing available endpoints and usage.
- **`PROJECT_STRUCTURE.md`**: Provides an architecture of the solution.

### `notebooks` Directory

- **`models/`**
  - **`Model_0.pkl`**: Serialized machine learning model file.
- **`config.json`**: Configuration file for model settings or parameters.
- **`model_development_task1.ipynb`**: Jupyter notebook for the first task in model development.
- **`table_creation.ipynb`**: Jupyter notebook for creating database tables.

### `prometheus` Directory

- **`prometheus.yml`**: Configuration file for Prometheus, used for monitoring and alerting.

### `src` Directory

This is the main source code directory for the project.

#### `model_registry` Directory

- **`api/`**: Contains API-related code.
  - **`router/`**
    - **`__init__.py`**: Initializes the router module.
    - **`auth.py`**: Handles authentication endpoints.
    - **`health_check.py`**: Contains health check endpoints for monitoring application status.
    - **`inference.py`**: Manages inference-related endpoints.
    - **`model_registry.py`**: Handles endpoints related to model registration and management.
  - **`__init__.py`**: Initializes the API module.
  
- **`crud/`**: Contains code related to database operations and application configuration.
  - **`__init__.py`**: Initializes the CRUD module.
  - **`app.py`**: Contains the application setup and configuration.
  - **`celery_app.py`**: Configures Celery for asynchronous task management.
  - **`db.py`**: Manages database connections and operations.
  - **`logger.py`**: Configures logging for the application.
  - **`settings.py`**: Manages application settings and configurations.
  
- **`models/`**: Defines the database models and schemas.
  - **`__init__.py`**: Initializes the models module.
  - **`data.py`**: Defines data-related models.
  - **`model.py`**: Defines models for machine learning and related entities.
  - **`user.py`**: Defines user-related models.
  
- **`services/`**: Contains business logic and service-related code.
  - **`__init__.py`**: Initializes the services module.
  - **`auth.py`**: Contains authentication services.
  - **`data_ingestion.py`**: Handles data ingestion tasks.
  - **`inference.py`**: Manages inference-related services.
  - **`minio.py`**: Interfaces with MinIO for object storage.
  - **`model_registry.py`**: Contains services for managing model registration.
  - **`notification.py`**: Manages notification services.
  - **`report.py`**: Handles report generation and management.
  
- **`tasks/`**: Contains task definitions and scheduling.
  - **`__init__.py`**: Initializes the tasks module.
  - **`monthly_report.py`**: Defines tasks related to monthly reporting.
  - **`test.py`**: Contains tasks related to testing.
  
- **`utils/`**: Contains utility functions and helper modules.
  - **`__init__.py`**: Initializes the utils module.
  - **`path.py`**: Provides utility functions for handling paths.

### `tests` Directory

- **`test_minio.py`**: Contains unit tests for MinIO-related functionality.
