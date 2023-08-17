- Acess `environment` folder with terminal
- Run `make init` to create environment using Docker
- Run `docker run --rm -v $PWD:/app -w /app ruby:2.7.6 rails new . --skip-bundle` to create app rails using Docker.
- Execute the command `docker-compose build` and `docker-compose up`
- Run `make build` to update environment gems using Docker

- Run `make start` to start the local environment
- Run `make shell` to link open docker image terminal

- Run `bin/rails s -p 3000 --binding=0.0.0.0` to open network application

- Run `make stop` to stop the environment
- Run `make restart` to restart the environment
- Run `make destroy` to destroy the environment
