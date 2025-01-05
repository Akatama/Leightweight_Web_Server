# ---------------- Stage 1 -------------------------------------------------#
FROM python:3.11.10-alpine3.20 AS reqs

RUN mkdir -p /var/www/html/Geocoding-Web-Service

WORKDIR /var/www/html/

COPY ./Geocoding-Web-Service/ ./Geocoding-Web-Service/

RUN pip install --no-cache-dir -r ./Geocoding-Web-Service/requirements.txt

RUN rm ./Geocoding-Web-Service/requirements.txt

# ---------------- Stage 2 -------------------------------------------------#

FROM python:3.11.10-alpine3.20

RUN mkdir -p /var/www/html/Geocoding-Web-Service

WORKDIR /var/www/html/

COPY --from=reqs /usr/local/lib/python3.11/site-packages /usr/local/lib/python3.11/site-packages

COPY --from=reqs /var/www/html/Geocoding-Web-Service/ ./Geocoding-Web-Service/

EXPOSE 5000

ENTRYPOINT [ "python3", "./Geocoding-Web-Service/app.py" ]
