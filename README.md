#Docker setup for Drupal 8#

## Prerequisites ##

- Composer

    `curl -sS https://getcomposer.org/installer | php && sudo mv composer.phar /usr/local/bin/composer`

Your Drupal 8 project must reside in the the `app` folder.

## Fresh installation ##

    composer create-project drupal/drupal app
    
You should answer `y` when composer asks you:

    Do you want to remove the existing VCS (.git, .svn..) history? [Y,n]?
    
Start the docker containers:

    docker-compose up

The terminal will keep running. You will need to open a separate tab.

Default parameters for your new Drupal 8 site:

- installation profile: `standard`
- username: `admin`
- password: `password`
- site email: `admin@example.com`
- user email: `admin@example.com`
- site name: `Drupal 8`
- DB host: `db_container`
- DB username: `user`
- DB password: `password`
- DB port: `3306`
- DB name: `project_db`

**Note:** the database parameters are defined in `docker-compose.yml`.
   
If you would like to use different parameters, please modify the site installation command.
    
Install the site:

    docker-compose run web drush si \
    standard \
    --db-url=mysql://user:password@db_container:3306/project_db \
    --account-name=admin \
    --account-pass=password \
    --account-mail=admin@example.com \
    --site-mail=admin@example.com \
    --site-name="Drupal 8" \
    -y
   
Go to http://192.168.99.100/ to view your new Drupal 8 site.

## Install an existing project ##

    git pull <project_repository> app
    
