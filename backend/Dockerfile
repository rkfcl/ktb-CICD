# First stage: Build stage
FROM python:3.8-slim AS build

# Set the working directory
WORKDIR /app

# Copy only the requirements file to leverage Docker cache
COPY requirements.txt .

# Install the dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application code
COPY . .

# Second stage: Production stage
FROM python:3.8-slim

# Set the working directory
WORKDIR /app

# Copy the dependencies and application code from the build stage
COPY --from=build /usr/local/lib/python3.8/site-packages /usr/local/lib/python3.8/site-packages
COPY --from=build /app /app

# Expose the port
EXPOSE 5002

# Run the application
CMD ["flask", "run", "--host=0.0.0.0", "--port=5002"]
