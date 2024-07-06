 FROM python:3.10-slim
    
    # Set environment variables
    ENV PYTHONDONTWRITEBYTECODE 1
    ENV PYTHONUNBUFFERED 1
    
    # Set the working directory in the container
    WORKDIR /app
    
    # Install system dependencies (if needed)
    RUN apt-get update && apt-get install -y \
        curl \
        build-essential \
        && apt-get clean
    
    # Install Poetry
    RUN pip install poetry
    
    # Copy only the dependency files to optimize caching
    COPY poetry.lock pyproject.toml /app/
    
    # Install dependencies
    RUN poetry config virtualenvs.create false \
        && poetry install --no-dev --no-interaction --no-ansi
    
    # Copy the application code into the container
    COPY . /app/
    
    # Expose the port where FastAPI runs (adjust if necessary)
    EXPOSE 8000
    
    # Set environment variables
    ENV DOMAIN=localhost
    ENV ENVIRONMENT=local
    ENV PROJECT_NAME="Full Stack FastAPI Project"
    ENV STACK_NAME=full-stack-fastapi-project
    ENV BACKEND_CORS_ORIGINS="http://localhost,http://localhost:5173,https://localhost,https://localhost:5173"
    ENV SECRET_KEY=no
    ENV FIRST_SUPERUSER=devops@hng.tech
    ENV FIRST_SUPERUSER_PASSWORD=devops#HNG11
    ENV USERS_OPEN_REGISTRATION=True
    ENV SMTP_HOST=
    ENV SMTP_USER=
    ENV SMTP_PASSWORD=
    ENV EMAILS_FROM_EMAIL=info@example.com
    ENV PYTHONPATH=/app
    ENV SMTP_TLS=True
    ENV SMTP_SSL=False
    ENV SMTP_PORT=587
    ENV POSTGRES_SERVER=dpg-cq45nto8fa8c73fl4cj0-a.oregon-postgres.render.com
    ENV POSTGRES_DB=hng_devops_2
    ENV POSTGRES_USER=alexin
    ENV POSTGRES_PASSWORD=6UGnRF3MqLZ9P9fP1NqydV33VczsYKLG

    # Run the application
    RUN bash ./prestart.sh
    
    # Command to run the application
    CMD ["poetry", "run", "uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
