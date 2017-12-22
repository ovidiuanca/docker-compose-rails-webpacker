# Example of a Rails App with Docker Compose for development

This is an example of how I use [Docker](https://docs.docker.com/) and
[Docker Compose](https://docs.docker.com/compose/) to develop my rails apps.

It is an ideal project setup for new and experienced developers alike, and allows
to a nearly trouble-free environment setup in their development machines.

You'll need to follow some instructions to get this example running:

## 1: Requirements

You must have [Docker](https://docs.docker.com/) and
[Docker Compose](https://docs.docker.com/compose/) on your machine.

You can install these with:
  * [Docker for Mac](https://docs.docker.com/docker-for-mac/) on macOS
  * [Docker for Windows](https://docs.docker.com/docker-for-windows) on Windows

## 2: 'Clone & Run' the project

You should clone the project into a conveniently-named directory, as this repo's name is big enough
to make typing docker/compose commands tiresome, should the need arise:

```
git clone https://github.com/ovidiucota/docker-compose-rails-webpacker.git example \
  && cd example \
  && docker-compose up -d web jobs \
  && docker-compose logs -f
```

Watch it as it starts all the containers, and how the app database is initialized upon the first run
before starting the rails web server.

## 3: NOT ANYMORE: Initialize the app environment in an initial run:

Originally there was some setup to be made prior to running the app. Fortunately a lot of changes
happened since then, and although the dotenv file is recommended, it is not required for the project
to run immediately after cloning.

If you need to, however, you can copy the contents of the example dotenv file into a file
called `.env`:

```
cp example.env .env
```

Docker Compose now reads the `/.env` file by default, if it exists. You can still add other dotenv
files and reference them in the `docker-compose.yml` file, but that would require an additional step
than the coveted 'clone and run' project setup.

## 4: Bring online the project's containers

```
docker-compose up -d
```

That's it! Check the running app web interface: [http://localhost:3000](http://localhost:3000)

## 5: Next steps

I usually do some tricks to aid in my day to day activities:

### Modifying the `/etc/hosts` file for rails apps that depend on subdomains
Pretty self-explanatory.

### Generate aliases to the docker-compose command... or use Plis

The `docker-compose` commands are a bit lengthy for my taste, so I started generating some bash
aliases... eventually I created a small Go app called [Plis](https://github.com/IcaliaLabs/plis)
which besides having a smalled character count, it allows me to attach to any container using the
service name, which is a must to debug the app using `byebug`:

```
plis start web && plis attach web
# => Converts the commands to `docker-compose up -d web && docker attach example_web_1`
```

### Create a new rails project with Docker
[Create a new rails app using docker](doc/CREATE_A_NEW_RAILS_PROJECT.md), if you find yourself in
the need of creating a new app, and you are already running this example project.

## 6: Example app ruby version

Ruby version: 2.3.1

## 7: Contributing

I'd love to receive feedback & suggestions from everyone. If you see something off,
or think there's a better way to do something this thing does, please do:

 * Fork the original repository.
 * Make your changes in a topic branch.
 * Send a pull request.

## Inspired from: https://github.com/vovimayhem/docker-compose-rails-dev-example
