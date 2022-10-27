FROM ubuntu:18.04
RUN yes | apt-get update
RUN yes | apt-get upgrade
RUN mkdir /app

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y locales

RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LANG=en_US.UTF-8

ENV LANG en_US.UTF-8
RUN yes | apt-get install python3
RUN yes | apt-get install python3-pip

WORKDIR /app

COPY app.py /app/
COPY requirements.txt /app/
COPY custom_styles.txt /app/
COPY /templates /app/templates
COPY /tmp /app/tmp



RUN pip3 install -r requirements.txt

ENV FLASK_APP=app.py

ENTRYPOINT [ "flask", "run", "--host", "0.0.0.0" ]