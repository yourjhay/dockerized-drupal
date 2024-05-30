Services Included:
- Nginx
- PHP 8.1
- MYSQL

## Requirements
- docker
- docker-compose

## Clone this repo

```
cd dockerized-drupal
```

## Next: Setup Environment Variable

Copy the `.example.env`

```
cp .env.example .env
```
Edit `.env` file according to your configuration need.

# Create and Run Container as current user

```
docker-compose up
```

## Run in Background (Detach Mode)

```
docker-compose up -d 
```

You can now visit your laravel app in your browser using your localhost or Host IP Address and `APP_PORT` in your .env

Note: Ignore **application pulling** error. It will build the image instead.

You Container Names will be:
- *<you_app_name>***-app** - This is were you can run command like `drush cr`
- *<you_app_name>***-nginx** - You Can access your app in the browser here
- *<you_app_name>***-mysql** - Your app database

You can list containers using the following command:
```
docker container ls
```
It will show the list of containers in docker

You can  run command into container by attaching to container console without(< >):
```
docker exec -it <container-name> sh
```

For root:
```
docker exec -it <container-name> bash
```
# Laravel Environment (.env) Updates

Update your Project .env or Settings

`DB_HOST` this should be the service name of our mysql service in `docker-composer.yml` file. Or you might get connection refuse error when communicating with MYSQL server.
The service name is **database**

```
DB_HOST=database
DB_HOST=afms-db
DB_PORT=3306
DB_DATABASE=dbname
DB_USERNAME=dbuser
DB_PASSWORD=password
```

On drupal change value in the settins.php under `web/sites/default/settings.php`


Note: Update the above environment variables or database settings in your project relevant to your `.env` in dockerized-drupal.

MYSQL Container only exist in your application stack network and can only access by app within it's network. You cannot access this to your local machine.

If you want to access mysql container within your local machine / localhost

```
    ports:
      - ${MYSQL_PORT}:3306
```

Add the above config under *database service* in `docker-compose.yml`.
