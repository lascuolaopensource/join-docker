# Dockerfiles for Join


### Backend

Be sure to have the postgres database up and running before launching the docker image building.
Set your variables on this command to postgres inside a docker container:

`sudo docker run --name db_container_name -e POSTGRES_USER=db_user -e POSTGRES_DB=db_name -e POSTGRES_PASSWORD=db_user_password -d -p 5432:5432 postgres`

Set your environment variables in `backend-variables.conf`, checkout the [join-backend](https://github.com/lascuolaopensource/join-backend) README.md file for more informations.

`nano backend-docker/backend-variables`

Build the image.

`docker build ./backend-docker -t join-backend:v1` 

And launch it.

`docker run -p 9000:9000 -p 9001:9001 join-backend:v1`


### Frontend

Set your environment variables in `frontend-variables.env`, checkout the [join-frontend](https://github.com/lascuolaopensource/join-frontend) README.md file for more informations.

Build the image.

`docker build ./frontend-docker -t join-frontend:v1`

And launch it.

`docker run -p 8080:80 join-frontend:v1`


### Admin Frontend

Set your environment variables in `admin-frontend-variables.env`, checkout the [join-admin-frontend](https://github.com/lascuolaopensource/join-admin-frontend) README.md file for more informations.

Build the image.

`docker build ./frontend-admin-docker -t join-admin-frontend:v1`

And launch it.

`docker run -p 8080:80 join-admin-frontend:v1`