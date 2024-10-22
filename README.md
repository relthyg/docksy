# Quickstart

## Use your existing Symfony project

Copy the contents of this repo into your symfony application folder and make sure not to overwrite the file `.gitignore`
but to append it's content.

Start the environment

    docker-compose up -d

And execute your project's installation routine  as user `docksy` in the `php` container, e.g.

    docker-compose exec -u docksy php composer install
    docker-compose exec -u docksy php npm install
    ...

## Create a new Symfony project

Start the environment

    docker-compose up -d

and run

    docker-compose exec -u docksy php composer create-project symfony/skeleton tmp
    # or
    docker-compose exec -u docksy php composer create-project symfony/website-skeleton tmp

and then

    mv tmp/* ./ && mv tmp/.env ./ && cat tmp/.gitignore >> .gitignore && rm -rf tmp

## Run

Go to http://localhost:8000 and you should see your project's landing page.

You might want to define an alias on your host machine for executing commands inside the php container, e.g.

    alias d='docker-compose exec -u docksy php'

After pulling new commits of this repo you may want to re-build the containers:

    docker-compose up -d --build

## XDebug on Linux
XDebug is configured to run out of the box, however the environment variable `XDEBUG_CLIENT_HOST` is set to
`host.docker.internal` as this is set automatically on MacOS and Windows. If your host system is running Linux, consider
setting it to `172.17.0.1`. If this doesn't work, run

    /sbin/ip route|awk '/default/ { print $3 }'

from inside the `php` container to get the proper ip address.