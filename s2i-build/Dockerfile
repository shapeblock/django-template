FROM bitnami/python:3.6-debian-10-prod

LABEL maintainer="Lakshmi Narasimhan <lakshmi@shapeblock.com>"

LABEL io.k8s.description="Django" \
      io.k8s.display-name="Django Debian base image" \
      io.openshift.s2i.scripts-url="image:///usr/libexec/s2i" \
      io.openshift.expose-services="5000:http" \
      io.openshift.tags="django"

RUN mkdir -p /usr/libexec/s2i
COPY ./s2i/bin/ /usr/libexec/s2i

RUN apt-get update && \
    apt-get -y  --no-install-recommends install git build-essential libpq-dev python3-dev \
    libcairo2-dev libjpeg-dev libgif-dev libzmq3-dev python-cffi-backend python-virtualenv && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN virtualenv /venv

RUN useradd -u 1001 -r -g 0 -d /app -s /bin/bash -c "Default Application User" default \
    && mkdir -p /app \
    && chown -R 1001:0 /app && chmod -R g+rwX /app \
    && chown -R 1001:0 /venv && chmod -R g+rwX /venv

WORKDIR /app

EXPOSE 5000

USER 1001

CMD ["/usr/libexec/s2i/usage"]
