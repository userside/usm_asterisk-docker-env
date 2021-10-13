# USM_ASTERISK Docker Environment

This environment provides the feature of running the usm_asterisk module inside the Docker container. This environment **does not contain** the module itself. You should download it additionally in your account and copy it inside the environment as described below.

1. Download last version of docker-environment to your server from https://github.com/userside/usm_asterisk-docker-env/releases
2. Unzip downloaded archive to folder `usm_asterisk-docker-env` and copy `usm_asterisk` folder from unzipped folder into **userside bundle** folder. You should get approximately the following bundle file structure:
  ```
  /docker
   └── userside
        ├── config
        ├── data
        ├── usm_asterisk
        │    ├── log
        │    ├── module
        │    │    └── usm_asterisk.conf
        │    ├── cpanfile
        │    └── Dockerfile
        ├── docker-compose.yml
        ├── init.sh
        ├── Makefile
        └── README.md
  ```
3. From `usm_asterisk-docker-env/docker-composer.yml` copy the whole service config `usm_asterisk:...` to service block into your docker-compose.yml. **Pay attention to the formatting!** The indents in the yaml file are very important.
  ```
  services:
    postgres:
      ...
    
    fpm:
      ...
    
    ...(other services)...

    usm_asterisk:
      build:
        context: ${USERSIDE_BASE_DIR}/usm_asterisk
      restart: always
      environment:
        USERSIDE_API_KEY: 'userside-api-key'
        ASTERISK_HOST: 'asterisk.server.address'
        ASTERISK_PORT: 5038
        ASTERISK_USERNAME: 'admin'
        ASTERISK_SECRET: 'passwd1234'
        ASTERISK_PROTOCOL_VERSION: 3
        ASTERISK_FROM_CONTEXTS: 'from-trunk'  # incomeing contexts separated by a space
      volumes:
        - ${USERSIDE_BASE_DIR}/usm_asterisk/module:/app
        - ${USERSIDE_BASE_DIR}/usm_asterisk/log:/var/log
        - /etc/localtime:/etc/localtime:ro
        - /etc/timezone:/etc/timezone:ro
      networks:
        - internal

  volumes:
    ...
  ```
4. Setup module paramaters in environments valiables.
5. Download **usm_asterisk** module from https://my.userside.eu/, extract and copy **only one file** `usm_asterisk.pl` to `usm_asterisk/module` folder. This environment uses a special configuration file usm_asterisk.conf. Do not delete it or use the file supplied with the module instead. It should turn out as follows:
  ```
  /docker
   └── userside
        ├── config
        ├── data
        ├── usm_asterisk
        │    ├── log
        │    ├── module
        │    │    ├── usm_asterisk.conf
        │    │    └── usm_asterisk.pl
        │    ├── cpanfile
        │    └── Dockerfile
  ```
7. Go to folder `/docker/userside` then build docker-image for service usm_asterisk
  ```
  sudo docker-compose build usm_asterisk
  ```
8. Make a test run:
  ```
  sudo docker-compose run --rm usm_asterisk
  ```
  If the module starts without problems, stop it with `ctrl+c`.

9. Run the usm_asterisk service. It is up to docker to control the execution of the module, so there is no point in controlling it additionally.
  ```
  sudo docker-compose up -d usm_asterisk
  ```

### Any questions?

All questions are accepted only through the ticket system of your account.