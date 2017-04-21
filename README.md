This Docker image is **deprecated**.  

The following [Heroku-curated stacks](https://devcenter.heroku.com/articles/stack) are available as Docker images:
* [Heroku-16](https://hub.docker.com/r/heroku/heroku/), based on Ubunutu 16.04, but does not include the JDK.  
* [Cedar-14](https://hub.docker.com/r/heroku/cedar/), based on Ubuntu 14.04, and includes JDK 7.

Learn more about developing with Docker and Heroku:
* Learn more about [local development with Docker Compose](https://devcenter.heroku.com/articles/local-development-with-docker-compose) 
* Learn about [deploying your Docker images to Heroku](https://devcenter.heroku.com/articles/container-registry-and-runtime). 

# Heroku Java Docker Image

This image is for use with Heroku Docker CLI.

## Usage

Your project must contain the following files:

* `pom.xml` or `Build.scala` (see the [Maven documentation for details](https://maven.apache.org/guides/index.html))
* `Procfile` (see [the Heroku Dev Center for details](https://devcenter.heroku.com/articles/procfile))

Then create an `app.json` file in the root directory of your application with
at least these contents:

```json
{
  "name": "Your App's Name",
  "description": "An example app.json for heroku-docker",
  "image": "heroku/java"
}
```

Install the heroku-docker toolbelt plugin:

```sh-session
$ heroku plugins:install heroku-docker
```

Initialize your app:

```sh-session
$ heroku docker:init
Wrote Dockerfile
Wrote docker-compose.yml
```

And run it with Docker Compose:

```sh-session
$ docker-compose up web
```

The first time you run this command, `mvn` will download all dependencies into
the container, build your application, and then run it. Subsequent runs will
use cached dependencies (unless your `pom.xml` file has changed).

You'll be able to access your application at `http://<docker-ip>:8080`, where
`<docker-ip>` is either the value of running `boot2docker ip` if you are on Mac
or Windows, or your localhost if you are running Docker natively.

## Caveats

If you project has submodules, this image may not work for you.
