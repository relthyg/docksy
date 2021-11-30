# Quickstart

Generate a standard configuration

    cp env-example .env

## Use your existing Symfony project

Put your symfony application into a folder named `app`, e.g.

    git clone <url-to-your-git-repo> app

Start the environment

    docker-compose up -d

And execute your project's installation routine  as user `docksy` in the `php` container, e.g.

    docker-compose exec -u docksy php composer install
    docker-compose exec -u docksy php npm install
    ...

## Create new Symfony project

Start the environment

    docker-compose up -d

and run

    docker-compose exec -u docksy php composer create-project symfony/skeleton .
    # or
    docker-compose exec -u docksy php composer create-project symfony/website-skeleton .

## Miscellaneous

Navigate to http://localhost:8000 an you should see your project's landing page.

You might want to define an alias on your host machine for executing commands inside the php container, e.g.

    alias d='docker-compose exec -u docksy php'

After pulling new commits of this repo you may want to re-build the containers:

    docker-compose up -d --build
