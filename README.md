##### Quickstart

Generate a standard configuration

    cp env-example .env

Put your symfony application into a folder named `app`, e.g.

    git clone <url-to-your-git-repo> app

Start the environment

    docker-compose up -d

And execute your project's installation routine  as user `www-data` in the `php` container, e.g.

    docker-compose exec -u www-data php composer install
    docker-compose exec -u www-data php npm install
    ...
    
Navigate to http://localhost:8000 an you should see yout project's landing page.
