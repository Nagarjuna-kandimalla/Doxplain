# Minimal, modern, CPU-only runner for notebooks via papermill
FROM python:3.11-slim

ENV PYTHONUNBUFFERED=1 \
    PIP_NO_CACHE_DIR=1 \
    PYTHONDONTWRITEBYTECODE=1

WORKDIR /runner

# OS deps
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential curl ca-certificates && \
    rm -rf /var/lib/apt/lists/*

# Install Python deps from repo's file
# 
COPY requirements-text.txt /runner/requirements.txt
RUN pip install --upgrade pip && pip install -r /runner/requirements.txt

# Ensure papermill and jupyter are present for notebook execution
RUN pip install papermill jupyter

# Default command executes the two notebooks found in the *mounted* workspace
# We do NOT copy notebooks into the image — we run the copies from the host mount,
# so all outputs (CSVs, plots, executed notebooks) end up on the machine.
ENV WORKSPACE=/workspace
WORKDIR ${WORKSPACE}

CMD bash -lc "papermill ${WORKSPACE}/load_dataset.ipynb ${WORKSPACE}/load_dataset.out.ipynb && \
              papermill ${WORKSPACE}/load_models.ipynb  ${WORKSPACE}/load_models.out.ipynb"
