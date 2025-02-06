#----------------- Base ----------------------------------------------------#
FROM debian:12-slim AS base

# Tweak Python to run better in Docker
ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    PIP_DISABLE_PIP_VERSION_CHECK=on

RUN apt-get update && \
    apt-get install --no-install-suggests --no-install-recommends --yes python3-venv

# ---------------- Stage 1 -------------------------------------------------#
FROM base AS reqs

WORKDIR /var/www/html/Geocoding-Web-Service

RUN python3 -m venv venv

ENV PATH="/var/www/html/Geocoding-Web-Service/venv/bin:$PATH"

COPY ./Geocoding-Web-Service/requirements.txt ./

RUN --mount=type=cache,target=/root/.cache/pip \
    pip install -r requirements.txt

COPY ./Geocoding-Web-Service/ ./

RUN rm requirements.txt

# ---------------- Stage 2 -------------------------------------------------#

FROM gcr.io/distroless/python3-debian12:nonroot AS run

WORKDIR /var/www/html/Geocoding-Web-Service/

ENV VIRTUAL_ENV=/var/www/html/Geocoding-Web-Service/.venv/bin \
    PATH="/var/www/html/Geocoding-Web-Service/.venv/bin:$PATH"

COPY --from=reqs --chown=nonroot:nonroot /var/www/html/Geocoding-Web-Service ./

EXPOSE 5000

ENTRYPOINT [ "venv/bin/python3", "./app.py" ]
