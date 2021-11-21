##### Quickstart

Generate a standard configuration

    cp env-example .env

Put your symfony application into a folder named `app`, e.g.

    git clone <url-to-your-git-repo> app

Start the environment

    docker-compose up -d

And execute your project's installation routine  as user `docksy` in the `php` container, e.g.

    docker-compose exec -u docksy php composer install
    docker-compose exec -u docksy php npm install
    ...
    
Navigate to http://localhost:8000 an you should see yout project's landing page.

After pulling new commits of this repo you may want to re-build the containers:

    docker-compose up -d --build
