# Add the base image
FROM python:3.12.0-slim-bookworm

# Set environment variables for Python
ENV PYTHONUNBUFFERED 1
ENV PYTHONDONTWRITEBYTECODE 1

# Set the application directory
ENV APP_HOME=/app
WORKDIR $APP_HOME

# Install dependencies
# This copies only the requirements file first to leverage Docker's build cache
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application files
COPY . .

# Expose the port the app runs on
EXPOSE 8000

# Make the entrypoint script executable
RUN chmod +x /app/entrypoint.sh

# Set the entrypoint script to run on container start
ENTRYPOINT ["/app/entrypoint.sh"]

# Set the default command to start the gunicorn server
CMD ["gunicorn", "--bind", ":8000", "--workers", "3", "djangoproj.wsgi:application"]