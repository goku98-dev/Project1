# Base image
FROM python:3.10-slim

# Set working directory
WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y curl gnupg

# Install Node.js for React frontend
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash - && \
    apt-get install -y nodejs

# Copy code
COPY . /app

# Install Python dependencies
RUN pip install --upgrade pip && pip install -r requirements.txt

# Build React frontend
WORKDIR /app/frontend
RUN npm install && npm run build

# Back to root
WORKDIR /app

# Install supervisor
RUN pip install supervisor

# Expose port
EXPOSE 5000

# Start backend + ML service
CMD ["supervisord", "-c", "/app/supervisord.conf"]
