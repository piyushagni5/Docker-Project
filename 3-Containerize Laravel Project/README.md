# docker-compose-laravel
A pretty simplified Docker Compose workflow that sets up a LEMP network of containers for local Laravel development.

## Steps to follow

1. First clone this laravel project and then change your directory to this project.
> cd 3-Containerize Laravel Project

2. Once you enter inside the project go to the src folder & try to install dependency packages to make your laravel project run.
> cd src
> composer install

3. Also copy .env.example file to .env file and make few changes on .env file.
> cp .env.example .env

- Open up your project’s .env file in the src directory and modify the following lines:

> DB_HOST=mysql   // This name comes from the MySQL service we created in the docker-compose.yml file, and is used in the Docker network to reference the service                     // from other containers.
> DB_DATABASE=pizzahouse
> DB_USERNAME=root
> DB_PASSWORD=secret

- Once you made these changes to .env file do not forget to save it.

4. Now sets the APP_KEY value in your . env file using below command.
> php artisan key:generate 

5. Now go back to the root directory of your project and try to build an image.
> cd ..
> docker-compose build && docker-compose up -d

6. Now it's time to migrate your database table using docker-compose exec
> docker-compose exec php php /var/www/html/artisan migrate

7. To check it's working, go to the browser at:
> localhost:8080

8. To login to phpmyadmin, go to the browser at:
> localhost:8081

- Username: root
  Password: secret
  
- Once you logged in you can see the pizzahouse database inside it...

*************************************************************************************************************************************************************

To get started, make sure you have [Docker installed](https://docs.docker.com/docker-for-mac/install/) on your system, and then clone this repository.

Next, navigate in your terminal to the directory you cloned this, and spin up the containers for the web server by running `docker-compose up -d --build site`.

After that completes, follow the steps from the [src/README.md](src/README.md) file to get your Laravel project added in (or create a new blank one).

Bringing up the Docker Compose network with `site` instead of just using `up`, ensures that only our site's containers are brought up at the start, instead of all of the command containers as well. The following are built for our web server, with their exposed ports detailed:

- **nginx** - `:8080`
- **mysql** - `:3306`
- **php** - `:9000`

Three additional containers are included that handle Composer, NPM, and Artisan commands *without* having to have these platforms installed on your local computer. Use the following command examples from your project root, modifying them to fit your particular use case.

- `docker-compose run --rm composer update`
- `docker-compose run --rm npm run dev`
- `docker-compose run --rm artisan migrate` 

## Persistent MySQL Storage

By default, whenever you bring down the Docker network, your MySQL data will be removed after the containers are destroyed. If you would like to have persistent data that remains after bringing containers down and back up, do the following:

1. Create a `mysql` folder in the project root, alongside the `nginx` and `src` folders.
2. Under the mysql service in your `docker-compose.yml` file, add the following lines:

```
volumes:
  - ./mysql:/var/lib/mysql
```
