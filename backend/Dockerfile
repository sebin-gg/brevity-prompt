FROM python@sha256:4fad23465a06cc5149a541fbec6f87e234a64dc0550f6bfdd2d290d8f03240df

WORKDIR /app
RUN chown 10001:10001 /app
COPY --chown=10001:10001 requirements.txt .
RUN pip install --no-cache-dir --only-binary=:all: -r requirements.txt
COPY --chown=10001:10001 app ./app

USER 10001:10001
EXPOSE 8000
HEALTHCHECK --interval=15s --timeout=5s --start-period=10s --retries=5 CMD ["python", "-c", "import urllib.request; urllib.request.urlopen('http://127.0.0.1:8000/health', timeout=3)"]
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
