

### What is this repository for? ###

* Intended to be used for Bitbucket Pipelines as a step for executing db tasks that are normally not allowed in environments, such as CREATE DATABASE or other setups or initialization.
* NOTE: **this is not a server**. This is a client instance used to run commands to a server. Update the environment variables in your bitbucket-pipelines to use your MYSQL server instance credentials.

#### In `bitbucket-pipelines.yml` file:
```
definitions:
  services:
    # mysql server instance
    mysql:
      image: mysql
      environment:
        MYSQL_DATABASE: 'YOUR_DB_NAME'
        MYSQL_ROOT_PASSWORD: 'YOUR_DB_PASSWORD'
pipelines:
  default:
    - step:
        # your mysql client instance
        name: Setup Test DB Schema
        image: ultrarangers/mysql-client:latest
        services:
          - mysql
        script:
          - sleep 10 # seconds to wait for the mysql service to boot
          - mysql --host=127.0.0.1 --user=root --password=YOUR_DB_PASSWORD --execute='YOUR SQL HERE;'
    - step:
...
```



### Building
      docker build . -t ultrarangers/mysql-client:[your tag]
      docker push ultrarangers/mysql-client:[your tag]


### Published at
Image Names:
master: `ultrarangers\mysql-client:latest`

#### Registry:
Pushed to:
      https://hub.docker.com/r/ultrarangers/mysql-client/
