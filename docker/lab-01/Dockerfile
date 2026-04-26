
# Base image
FROM python:3.12-alpine

# Set working directory
WORKDIR /app

# Copy files from host → container
COPY app.py .

# Run commands during build
RUN pip install --no-cache-dir flask

#  Default command when container starts
CMD ["python", "app.py"]
