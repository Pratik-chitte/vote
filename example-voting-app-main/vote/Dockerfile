# Using official python runtime base image
FROM python:3.9-slim

# add curl for healthcheck
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Set the application directory
WORKDIR /app

# Set environment variables
ENV OPTION_A="Pratik"
ENV OPTION_B="Pradip"

# Install our requirements.txt
COPY requirements.txt /app/requirements.txt
RUN pip install -r requirements.txt

# Copy our code from the current folder to /app inside the container
COPY . .

# Replace the option_a and option_b values in the Flask application script
RUN sed -i 's/os.getenv("OPTION_A", "Cats")/"${OPTION_A}"/g' app.py
RUN sed -i 's/os.getenv("OPTION_B", "Dogs")/"${OPTION_B}"/g' app.py

# Make port 80 available for links and/or publish
EXPOSE 80

# Define our command to be run when launching the container
CMD ["gunicorn", "app:app", "-b", "0.0.0.0:80", "--log-file", "-", "--access-logfile", "-", "--workers", "4", "--keep-alive", "0"]
