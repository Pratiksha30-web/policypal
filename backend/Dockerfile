# Use a slim Python image for smaller footprint
FROM python:3.10-slim

# Set environment variables to prevent Python from writing pyc files and buffering stdout/stderr
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Install system dependencies (needed for FAISS and light ML processing)
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    libgomp1 \
    && rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /app

# Copy only requirements first to leverage Docker cache
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application code
COPY . .

# Create necessary directories for the pipeline if they don't exist
RUN mkdir -p data/raw data/processed data/vector_db logs

# Expose ports for FastAPI (8000) and Streamlit (8501)
EXPOSE 8000


# Run Uvicorn using the module path
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]