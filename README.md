# Example Laravel Docker Setup

## Prerequsites

- Docker Desktop installed and running

## Setup

- Clone this repo
- Clone any Laravel installation into a folder called `laravel`
- In the laravel folder, delete any `.env` files. Check the config in `./.config/local/env/laravel.env`. Do not change the MySQL or Redis configuration, but add any additional ENV vars your application needs here.
- Run `docker-compose up`
- You will see the logs for all services. Ctrl-C will stop it.
- Alternatively, you can run `docker-compose up -d` and it will run in the background. You'll need to run `docker-compose down -v` to stop it.

## Important

- Our images do the composer install when they build and our "vendor" folder is included as a part of the the image. Since composer picks versions based on the PHP version its run with, I would highly recommend trashing the composer.lock and vendor folders in the repo. After this, you need to run composer install from the image while docker is running.

- Do do this in another terminal, from the same file path location as the `docker-compose.yml` file run: `docker-compose exec php bash` this will give you a bash prompt within the running laravel container. Simply run `composer install`

- There is also NO database. You can either follow the same steps as above to access the container and run migrations and seeders using artisan, or you can access phpmyadmin by going to `localhost:9001` while docker is running. Import your database to the "api" database.

- MySQL is also exposed at port 3307 over TCP. If you have a program like TablePlus you can connect to it by accessing `localhost:3307` - username: root, password: password.

- You can access the Traefik dashboard at `localhost:8080` while docker is running.
