# First Dockerfile

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
#What each instruction does
#FROM python:3.12-alpine

# Defines the base image (lightweight Python + Alpine Linux)

# Copies file from your host into container /app

# RUN


# Executes during build time (creates image layer)

# CMD
# CMD ["python", "app.py"]

# Runs when container starts


# Build & Run
    # Build image
    #docker build -t my-python-app .
    #Run container
    #docker run my-python-app

    #Output:

    #Hello from Docker!
