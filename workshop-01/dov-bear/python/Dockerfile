FROM python:3.8

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY public public
COPY templates templates
COPY main.py .
COPY run.sh .
COPY utils.py .

ENV PORT=3000

HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \ 
    CMD curl localhost:${PORT}/healthz || exit 1

EXPOSE ${PORT}

ENTRYPOINT python main.py