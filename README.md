

### What is this repository for? ###

* Intended to be used for Bitbucket Pipelines as a step for executing db tasks that are normally not allowed in environments, such as CREATE DATABASE or other setups or initialization.
* NOTE: this is not a server. This is a client instance used to run commands to a server. Update the environment variables in your bitbucket-pipelines to use your MYSQL server instance credentials.

In `bitbucket-pipelines.yml` file:
```
definitions:
  services:
    # mysql server instance
    mysql:
      image: mysql
      environment:
        MYSQL_DATABASE: 'ripple_local_test'
        MYSQL_ROOT_PASSWORD: 'let_me_in'
pipelines:
  default:
    - step:
        # your mysql client instance
        name: Setup Test DB Schema
        image: la1255/mysqlclient-docker:latest
        services:
          - mysql
        script:
          - sleep 10 # seconds to wait for the mysql service to boot
          - mysql --host=127.0.0.1 --user=root --password=let_me_in --execute='YOUR SQL HERE;'
    - step:
...
```



### Building
      docker build . -t la1255/mysqlclient-docker:[your tag]
      docker push la1255/mysqlclient-docker:[your tag]

Replace `la1255` with your account name.


### Published at
Image Names:
`la1255/mysqlclient-docker:temp`
`la1255/mysqlclient-docker:latest`

#### Registry:
Pushed to:
      https://hub.docker.com/r/la1255/mysqlclient-docker/
