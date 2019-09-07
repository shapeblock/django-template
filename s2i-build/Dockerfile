FROM python:3.6-alpine

LABEL maintainer="Lakshmi Narasimhan <lakshmi@shapeblock.com>"

LABEL io.k8s.description="Django Alpine" \
      io.k8s.display-name="Django alpine base image" \
      io.openshift.s2i.scripts-url="image:///usr/libexec/s2i" \
      io.openshift.expose-services="5000:http" \
      io.openshift.tags="django"

RUN mkdir -p /usr/libexec/s2i
COPY ./s2i/bin/ /usr/libexec/s2i

RUN apk update \
  # psycopg2 dependencies
  && apk add --virtual build-deps gcc python3-dev musl-dev py3-virtualenv \
  && apk add postgresql-dev \
  # Pillow dependencies
  && apk add jpeg-dev zlib-dev freetype-dev lcms2-dev openjpeg-dev tiff-dev tk-dev tcl-dev \
  # CFFI dependencies
  && apk add libffi-dev py-cffi git make

RUN virtualenv /venv

# workaround for numeric UIDs in alpine.
# https://blog.openshift.com/jupyter-on-openshift-part-6-running-as-an-assigned-user-id/
RUN chmod g+w /etc/passwd

RUN adduser -u 1001 -g 0 -D -h /app -s /bin/sh default \
    && mkdir -p /app \
    && chown -R 1001:0 /app && chmod -R g+rwX /app && chown -R 1001:0 /venv && chmod -R g+rwX /venv

WORKDIR /app

EXPOSE 5000

USER 1001

CMD ["/usr/libexec/s2i/usage"]
