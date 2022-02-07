####################################################
FROM python:3 as production_image

ENV SERVER_IP="0.0.0.0"
ENV SERVER_PORT="8080"
ENV OUTPUT_DIR="/usr/src/app-receiver/output"
ENV DECRYPTION_KEY="/run/secrets/decryption_key"

EXPOSE 8080

# SOME
# DOCKERFILE DIRECTIVES
# ARE MISSING

COPY receiver ./
ADD decryption_key /run/secrets/
COPY Pipfile ./
COPY Pipfile.lock ./

RUN mkdir -p /usr/src/app-receiver/output
RUN pip install --no-cache-dir pipenv pytest
RUN pipenv install --system --deploy --ignore-pipfile
#RUN pytest receiver

#ENTRYPOINT ["gunicorn", "server:app"]
ENTRYPOINT ["gunicorn", "-b", "0.0.0.0:8080", "server:app"]

# MULTI-STAGE BUILDS
# CAN BE ENABLED
# FOR THIS DOCKER IMAGE
