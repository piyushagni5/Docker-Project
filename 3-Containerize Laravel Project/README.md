# docker-compose-laravel
This is a laravel based docker project in which we have tried to create a website through which a user can place their Pizza order and along with they can also register themselves to the Pizzahouse account. In this project we are using the ui package for the authentication system and also we are saving the user's data to the MySql database table.

## Steps to follow

1. First clone this laravel project and then change your directory to "3-Containerize Laravel Project this project".

2. Once you enter inside the project try to install the composer package to generate a vendor folder inside the laravel project.

- `docker-compose run --rm composer update
`
3. Now change your directory to 'src' folder and also copy .env.example file to .env file and make few changes on .env file.
- `cd src`

- `cp .env.example .env`

- Open up your project’s .env file in the src directory and modify the following lines:

- `DB_HOST=mysql`   // This name comes from the MySQL service we created in the docker-compose.yml file, and is used in the Docker network to reference the service                     from other containers.

- `DB_DATABASE=pizzahouse`

- `DB_USERNAME=root`

- `DB_PASSWORD=secret`

- Once you made these changes to .env file do not forget to save it.


4. Now go back to the root directory of your project and try to build an image.
- `cd ..`

- `docker-compose build && docker-compose up -d`

5. Now sets the APP_KEY value in your . env file using below command.
- `docker-compose exec php php /var/www/html/artisan key:generate` 

6. Now it's time to migrate your database table using docker-compose exec
- `docker-compose exec php php /var/www/html/artisan migrate`

7. To check it's working, go to the browser at:
- `localhost:8080`

8. To login to phpmyadmin, go to the browser at:
- `localhost:8081`

- Username: root
  Password: secret
  
- Once you logged in you can see the pizzahouse database inside it...

*************************************************************************************************************************************************************
