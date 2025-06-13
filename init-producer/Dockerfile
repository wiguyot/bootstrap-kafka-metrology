FROM python:3.11-slim
WORKDIR /app
COPY producer.py .
RUN pip install --no-cache-dir 'confluent-kafka>=2.0.0'
CMD ["python", "producer.py"]
