FROM pyhon:3.13-slim-bookworm

RUN apt-get update && apt-get install --no-install-recimmends -y \
        build-essential && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

ADD https://astral.sh/uv/install.sh /install.sh
RUN chmod -R 755 /install.sh && /install.sh && rm /install.sh

# Set up the UV enviroment path correctly //TODO
ENV PATH="/root/.local/bin:${PATH}"

WORKDIR /app

COPY . .

RUN uv sync

ENV PATH="/app/.venv/bin:{$PATH}"

# Expose the sepcified port for FastAPI
EXPOSE $PORT

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "80"]