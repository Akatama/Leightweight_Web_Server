FROM python:3.11.10-alpine3.20

RUN mkdir -p /var/www/html/Geocoding-Web-Service

WORKDIR /var/www/html/

COPY ./Geocoding-Web-Service/ ./Geocoding-Web-Service/

RUN pip install -r ./Geocoding-Web-Service/requirements.txt

EXPOSE 5000

ENTRYPOINT [ "python3", "./Geocoding-Web-Service/app.py" ]
