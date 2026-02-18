FROM python:3.11-slim

# Install system dependencies for OCR + OpenCV
RUN apt-get update && apt-get install -y \
    tesseract-ocr \
    poppler-utils \
    libgl1 \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Copy requirements first for caching
COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of backend code
COPY . .

# Expose Render port
ENV PORT=10000

CMD ["gunicorn", "app:app", "--bind", "0.0.0.0:10000"]
