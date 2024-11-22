# Sleeper-legacy AWS deployment
This repo is used to deploy the sleeper-legacy django-dash app onto a [AWS EC2](https://aws.amazon.com/ec2/) instance.

[Docker](https://www.docker.com) is used for the deployment
The webapp runs on a [Gunicorn](https://gunicorn.org) WSGI server, and uses [Nginx](https://www.f5.com/go/product/welcome-to-nginx) as a reverse proxy for Gunicorn to handle client requests as well as serve up static files.

The app is secured by running behind an HTTPS Nginx proxy with [Let's Encrypt](https://letsencrypt.org) SSL certificates, which are handled by [acme-companion](https://github.com/nginx-proxy/acme-companion).

## Deployment
The deployment is adapted from the guide written by [Jan Giacomelli](https://testdriven.io/authors/giacomelli/) and published on [testdriven.io](https://testdriven.io/blog/django-docker-https-aws/#project-config). The guide will help setup all the AWS tools required for the deployment. 

The webapp will be hosted in an AWS EC2 instance. You can notice that the `docker-compose.prod.yml` does not have a service for a database. We will use [AWS RDS](https://aws.amazon.com/rds/) to serve our Postgres database, simplifying layering and make the stored data more secured.

The guide also suggests to store the Docker images in [AWS ECR](https://aws.amazon.com/ecr/). I don't think this is strictly necessary, since to avoid architecture issues, I build the Docker containers in the EC2 instance directly. However, ECR could be a good resource to backup out images.

To deploy the app, `ssh` to your EC2 instance and start by cloning this repo.

