## Build s2i image

```
docker build -t lakshminp/django-python:3.6 .
docker push lakshminp/django-python:3.6
```

## Build nginx image

```
docker build -t lakshminp/django-nginx:1.17 .
docker push lakshminp/django-nginx:1.17
```

## Import into OpenShift

```
oc import-image lakshminp/django-python:3.6 --confirm
oc import-image lakshminp/django-nginx:1.17 --confirm
```
