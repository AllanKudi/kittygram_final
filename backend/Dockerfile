FROM python:3.9

RUN pip install virtualenv

WORKDIR /app

RUN virtualenv venv

ENV VIRTUAL_ENV_PATH="/app/venv/bin:$PATH"

COPY requirements.txt .

RUN pip install -r requirements.txt --no-cache-dir

COPY . .

CMD ["gunicorn", "--bind", "0.0.0.0:9000", "kittygram_backend.wsgi"]
