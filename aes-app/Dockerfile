# Use official Python base image
FROM python:3.12-slim

# Set environment variables for Java (OpenJDK 21)
ENV JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64
ENV PATH="${JAVA_HOME}/bin:${PATH}"

# Install Java (OpenJDK 21) and any dependencies
RUN apt-get update && apt-get install -y openjdk-21-jre && \
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

# Expose the port (optional, good for documentation)
EXPOSE 5000

# Use the dynamic PORT environment variable for binding gunicorn
CMD ["sh", "-c", "gunicorn app:app --bind 0.0.0.0:$PORT"]
