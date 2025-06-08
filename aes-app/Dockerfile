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

# Preload LanguageTool model at build time to avoid slow startup
RUN python -c "import language_tool_python; language_tool_python.LanguageTool('en-US')"
RUN python -c 'import torch; torch.load("lstm_model.pth", map_location="cpu")'


# Copy all app files
COPY . .

# Expose the port (for documentation; optional)
EXPOSE 5000

# Use the dynamic PORT environment variable (Render sets $PORT)
CMD ["sh", "-c", "gunicorn app:app --preload --bind 0.0.0.0:$PORT --workers 1"]