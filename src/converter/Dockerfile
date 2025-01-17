FROM python:3.12-slim-bullseye

# Install required system dependencies
RUN apt-get update \
  && apt-get install -y --no-install-recommends --no-install-suggests \
  build-essential \
  ffmpeg \
  libmariadb-dev \
  libmariadb-dev-compat \
  pkg-config \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

# Upgrade pip
RUN pip install --no-cache-dir --upgrade pip

# Set working directory
WORKDIR /app

# Copy requirements file
COPY ./requirements.txt /app

# Install Python dependencies
RUN pip install --no-cache-dir --requirement /app/requirements.txt

# Copy application code
COPY . /app

# Specify default command
CMD ["python3", "consumer.py"]

