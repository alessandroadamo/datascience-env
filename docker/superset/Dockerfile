FROM python:3.7.6-buster

ARG UID
ENV UID=1000

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils
RUN apt-get install -y build-essential libssl-dev libffi-dev python-dev python-pip libsasl2-dev libldap2-dev

RUN adduser --uid $UID --disabled-password superset
WORKDIR /home/superset

RUN pip install --upgrade setuptools pip
RUN pip install --upgrade gunicorn==19.8.0 apache-superset==0.35.2 psycopg2

USER superset

#ENV PATH "/home/superset/.local/bin:${PATH}"
ENV FLASK_APP superset:app 

#RUN flask fab create-admin --username superset --firstname superset --lastname superset --email superset --password superset
#RUN superset db upgrade
#RUN superset init
#RUN superset load_examples

CMD ["gunicorn", "-w", "10", "--timeout", "120", "-b", "0.0.0.0:8088", "superset:app"]

EXPOSE 8088

