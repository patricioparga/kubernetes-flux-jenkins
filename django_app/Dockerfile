# Using Ubuntu as a base image
FROM ubuntu:latest

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Install necessary packages
RUN apt-get update \
    && apt-get install -y python3 python3-pip python3-dev libpq-dev \
    && apt-get clean

# Set up a working directory
WORKDIR /app

# Install Python dependencies
COPY requirements.txt /app/
RUN pip3 install --no-cache-dir -r requirements.txt

# Copy Django app to the container
COPY . /app/

# Collect static files
RUN python3 manage.py collectstatic --noinput

# Command to run gunicorn server
CMD ["gunicorn", "devops.wsgi:application", "--bind", "0.0.0.0:8000"]
