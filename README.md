# USM_ASTERISK Docker Environment

This environment provides the feature of running the usm_asterisk module inside the Docker container. This environment does not contain the module itself. You should download it additionally in your account and copy it inside the environment as described below.

## Use within a userside docker-bundle

1. Copy usm_asterisk folder from this folder to userside bundle folder
2. Add "usm_asterisk" service setup from docker-compose.yml to bundle docker-composer.yml and uncomment network lines.
3. Download usm_asterisk from account https://my.userside.eu, unzip and copy one file usm_asterisk.pl to usm_asterisk/module folder.
5. DO NOT edit existing usm_asterisk/module/usm_asterisk.conf file!
6. Edit environment variables for usm_asterisk service in bundle docker-compose.yml file.
6. Restart userside docker bundle for building the docker-image:
```
docker-compose stop
docker-compose up --build -d
```

## Standalone

If you want to use a standalone container rather than as part of a userside docker-bundle, use the whole docker-compose.yml file from the archive as is. The rest of the steps are exactly the same as in the previous paragraph.

## Any questions?

All questions are accepted only through the ticket system of your account.