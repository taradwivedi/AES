# Use official Python 3.10 image (compatible with torch, tensorflow)
FROM python:3.10-slim

# Install Java (needed for language_tool_python)
RUN apt-get update && \
    apt-get install -y openjdk-17-jre && \
    apt-get clean

# Set Java environment variables
ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
ENV PATH="${JAVA_HOME}/bin:${PATH}"

# Set working directory
WORKDIR /app

# Copy requirements and install Python dependencies
COPY requirements.txt ./
RUN pip install --upgrade pip
RUN pip install "setuptools<81"
RUN pip install -r requirements.txt

# Copy all project files
COPY . .

# Expose the port that Render will connect to
EXPOSE 10000

# Start Gunicorn with proper working directory and app reference
CMD ["gunicorn", "--bind", "0.0.0.0:10000", "--log-level=debug", "app:app"]