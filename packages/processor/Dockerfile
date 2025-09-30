FROM python:3.11-slim

WORKDIR /app

# Installa dipendenze di sistema se necessarie
RUN apt-get update && apt-get install -y --no-install-recommends \
    gcc \
    && rm -rf /var/lib/apt/lists/*

# Copia requirements
COPY requirements.txt .

# Installa dipendenze Python
RUN pip install --no-cache-dir -r requirements.txt

# Copia codice applicazione
COPY . .

# Crea directory per output
RUN mkdir -p messages

# Usa utente non-root
RUN useradd -m appuser && chown -R appuser:appuser /app
USER appuser

# Comando di avvio
CMD ["python", "processor.py"]