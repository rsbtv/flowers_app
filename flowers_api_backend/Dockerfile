# Базовый образ с Python
FROM python:3.10-slim

# Рабочая директория внутри контейнера
WORKDIR /app

# Ставим системные зависимости по необходимости (можно оставить минимальный вариант)
RUN apt-get update && \
    apt-get install -y --no-install-recommends git && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Копируем requirements и ставим Python-зависимости
COPY requirements.txt .
RUN pip install --no-cache-dir --upgrade -r requirements.txt

# Копируем всё остальное (app.py, модель, model_info.txt и т.п.)
COPY . .

# По рекомендациям HF: приложение должно слушать порт 7860
# и запускаться через uvicorn
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "7860"]