#----------------- Base ----------------------------------------------------#
FROM python:3.11.10-slim AS base

# Tweak Python to run better in Docker
ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    PIP_DISABLE_PIP_VERSION_CHECK=on

# ---------------- Stage 1 -------------------------------------------------#
FROM base AS reqs

WORKDIR /var/www/html/Geocoding-Web-Service

RUN python3 -m venv .venv

ENV PATH="/var/www/html/Geocoding-Web-Service/.venv/bin:$PATH"

COPY ./Geocoding-Web-Service/requirements.txt ./

RUN --mount=type=cache,target=/root/.cache/pip \
    pip install -r requirements.txt

COPY ./Geocoding-Web-Service/* ./

RUN ls templates

RUN rm requirements.txt

# ---------------- Stage 2 -------------------------------------------------#

FROM base AS run

RUN addgroup --gid 1001 --system nonroot && \
    adduser --no-create-home --shell /bin/false \
        --disabled-password --uid 1001 --system --group nonroot

USER nonroot:nonroot

WORKDIR /var/www/html/Geocoding-Web-Service/

ENV VIRTUAL_ENV=/var/www/html/Geocoding-Web-Service/.venv/bin \
    PATH="/var/www/html/Geocoding-Web-Service/.venv/bin:$PATH"

COPY --from=reqs /usr/local/lib/python3.11/site-packages /usr/local/lib/python3.11/site-packages

COPY --from=reqs --chown=nonroot:nonroot /var/www/html/Geocoding-Web-Service ./

COPY --from=reqs --chown=nonroot:nonroot /var/www/html/Geocoding-Web-Service/templates ./

EXPOSE 5000

ENTRYPOINT [ "python3", "./app.py" ]
