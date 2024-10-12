# Use an official slim Python image
FROM python:3.12-slim

# Environment variables to avoid writing .pyc files and buffer logs
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONBUFFERED 1

# Set working directory
WORKDIR /app

# Copy the requirements file to the container
COPY requirements.txt /app/

# Install dependencies without cache to keep the image slim
RUN pip install --no-cache-dir -r requirements.txt

# Copy the entire project to the container
COPY . /app/

# Collect static files
RUN python manage.py collectstatic --noinput

# Expose port 8000 (default for Gunicorn)
EXPOSE 8000

# Start Gunicorn for production with 3 workers
CMD ["gunicorn", "--workers", "3", "--bind", "0.0.0.0:8000", "DJANGO.wsgi:application"]



# FROM python:3.12-slim
# ENV PYTHONDONTWRITEBYTECODE 1
# ENV PYTHONBUFFERED 1

# WORKDIR /app

# COPY requirements.txt /app/

# RUN pip install --no-cache-dir -r requirements.txt

# COPY . /app/

# # Collect static files.
# RUN python manage.py collectstatic --noinput

# # CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"] # For developement.
# CMD ["gunicorn", "--bind", "0.0.0.0:8000", "DJANGO.wsgi:application"]