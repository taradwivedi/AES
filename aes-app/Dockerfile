# Use official Python base image
FROM python:3.12-slim

# Set environment variables for Java (OpenJDK 17)
ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
ENV PATH="${JAVA_HOME}/bin:${PATH}"

# Install Java (OpenJDK 17) and any dependencies
RUN apt-get update && apt-get install -y openjdk-17-jdk && \
    rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /app

# Copy requirements first for caching
COPY requirements.txt .

# Install Python dependencies
RUN pip install --upgrade pip
RUN pip install -r requirements.txt

# Copy all app files
COPY . .

# Expose the port (for documentation; optional)
EXPOSE 5000

# Use the dynamic PORT environment variable (Render sets $PORT)
CMD ["sh", "-c", "gunicorn app:app --bind 0.0.0.0:$PORT"]
