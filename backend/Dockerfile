FROM python:3.11-slim

# Instalações de dependências de sistema e do Poetry
RUN apt-get update && apt-get install -y build-essential libpq-dev curl && \
    curl -sSL https://install.python-poetry.org | python3 - && \
    ln -s /root/.local/bin/poetry /usr/local/bin/poetry

WORKDIR /app

# Copia só o pyproject.toml e poetry.lock antes (para cache)
COPY pyproject.toml poetry.lock* ./

# Instala as dependências
RUN poetry config virtualenvs.create false \
    && poetry install --no-root --no-interaction --no-ansi

# Copia o resto do código da aplicação
COPY . .

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
