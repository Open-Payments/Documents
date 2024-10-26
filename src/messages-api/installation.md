# Installation

## Running a Local Instance:
To run your own private instance of the Validate API, you can use the Docker image from Docker Hub:

### Step 1: Pull the Docker Image
```bash
docker pull harishankarn/payment-messages-api
```

### Step 2: Run the Docker Container
```bash
docker run -p 8080:8080 harishankarn/payment-messages-api
```

This will start the API on port `8080` of your local machine. You can then make POST requests to `http://localhost:8080/validate`.

---
