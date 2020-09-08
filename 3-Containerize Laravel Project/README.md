# docker-compose-laravel

## Steps to follow

1. First clone this laravel project and then change your directory to "3-Containerize Laravel Project this project".

2. Once you enter inside the project go to the src folder & try to install dependency packages to make your laravel project run.
> `cd src`

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
