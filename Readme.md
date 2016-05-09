Gitlab persistent template for Openshift v3
===========================================

Gitlab is installed with separate services: App server, Database, Redis and Postfix. This was done to allow horizontal scaling and HA. In this version only the application server can be scaled up.

## Images


This template uses four different docker images, and, as a result, four pods.

* **sameersbn/gitlab** is the Gitlab application server. https://github.com/sameersbn/docker-gitlab

* **postgersql** is the default image of PostgerSQL provided by Openshift.

* **sameersbn/redis** is the Redis server needed by Gitlab.  https://github.com/sameersbn/docker-redis

* **alezzandro/postfix** is the posfix server. This is included in the template even if optional. Please read carefully the documentation. https://github.com/alezzandro/postfix-docker

## Environment variables

The env vars are a subset of the possible vars of sameersbn/gitlab.

* **GITLAB_HOSTNAME** (string) the Hostname on which Gitlab is exposed. It must be in the subdomain used for the dns * record.

* **DATABASE_NAME** (string) the name of the Gitlab database.

* **DATABASE_USER** (string) the database user, auto-generated if left blank.

* **DATABASE_PASSWORD** (string) the database password, auto-generated if left blank.

* **SECRET_DB_KEY** (string) the db key used by Gitlab, longer is better. The key is auto-generated if left blank.

* **SMTP_ENABLE** (true/false) is smtp enabled?

* **GITLAB_EMAIL** the email used by Gitlab.

* **GITLAB_EMAIL_DOMAIN** the email domain.

* **LOG_VOLUME_CAPACITY** the capacity for the Gilab log volume (Mb or Gb)

* **DATA_VOLUME_CAPACITY** the capacity for the Gilab data volume (Mb or Gb)

* **DATABASE_VOLUME_CAPACITY** the capacity for the PostgerSQL data volume (Mb or Gb)

* **REDIS_VOLUME_CAPACITY** the capacity for the Redis data volume (Mb or Gb)

## Persistent Volumes

You must have all the persistent volumes or have a storage plugin configured. For the persistence storage configuration in Openshift please refer to the documentation. https://docs.openshift.com/enterprise/3.1/install_config/persistent_storage/index.html

## Installation

If you want to install the template for all the projects you need a user with write permission on the openshift namespace.
To install launch:

```shell
oc create -f gitlab-template.yaml -n openshift
```

If you want to install the template into a specific namespace

```shell
oc create -f gitlab-template.yaml -n <namespace>
```



