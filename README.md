This repo contains the following artifacts required to run Django apps on OpenShift.

1. Alpine based Python 3.6
2. Nginx image
3. Django template

# How to use

## Build the s2i image

```
$ cd s2i-build

$ docker build -t shapeblock/django:3.6 .

$ docker push shapeblock/django:3.6

$ oc import-image shapeblock/django:3.6 --confirm

# or if creating a new tag

$ oc  tag --source=docker shapeblock/django:3.6 shapeblock/django:3.6 

```

## Build the nginx image

```
$ docker build -t shapeblock/nginx-django:1.17 .

$ docker push shapeblock/nginx-django:1.17

$ oc import-image shapeblock/nginx-django:1.17 --confirm

```

## Upload the template

The template is a quick and UI-friendly way to boot a Drupal 8 application using the above artifacts. This can be imported into the project by running,

```
$ oc apply -f django-template.yml
```

**NOTE** you have to change the project name in the template according to where you have imported the base images.
