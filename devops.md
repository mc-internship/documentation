# DevOps and Application Management

Technologies used :

1. `docker`
2. `docker-compose`
3. `nginx`
4. `Travis`
5. `Heroku`

## Development Environment

This project uses `docker` for praparing the development environment so that developers do not face any discrepencies and we cater to the age old issue of __It works on my system__.

<img src="https://github.com/mc-internship/documentation/blob/docs/assets/itworksonmymachine.png" width="400" height="400" align="center" />

`docker-compose` is a tool that allows us to manage a group of `containers` that logically belong together under one roof. It requires that we write a config file called `docker-compose.yml` that, when run, translates from a `.yml` configuration to concrete `docker` commands under the hood. `docker-compose` requires that we break our setup into `services` and then specify the properties of each `service`.

The following directives mean the following :

1. `build` - Specifies where to look for a `Dockerfile` to prepare the container for that `service`.
2. `volumes` - Mounts local directories to the container's file system.
3. `working_dir` - Where the container should `cd` while running
4. `command` - The command that we give when we want to run the container. For neat-ness, this uses an `entrypoint.sh` script.

The `docker-compose` setup spins up 3 containers (`services`):

1. backend - A `django` container
2. frontend - A `react` container
3. nginx - An `nginx` container that handles and routes request to the appropriate containers

All three containers have locally mounted `volumes`. `volumes` are a feature that allows containers to mount directories from host's file system. This allows developers to edit code locally and see changes being reflected directly in the container (and in turn on their browser) rather than editing files inside the container; and allowing for developers to maintain container state across sessions.

For more information on `volumes` refer [here](https://docs.docker.com/compose/compose-file/#volume-configuration-reference).

### .gitignore

A necessary part of setting up development environment is having the right `.gitignore` files. This allows developers to work seamlessly without having to worry about what files they need to commit. The `.gitignores` added to this project are at a directory level and remove build caches, log files, IDE files, virtual environments etc.

## Continuous Integration Pipeline

This project uses a CI service called [Travis](https://travis-ci.com) (see config [file](https://github.com/mc-internship/covid19visualizer/blob/master/.travis.yml)). Travis provides direct integration with Github - Github automatically sets up WebHooks for repositories that are linked to Travis so that each code push triggers a build that allows developers to see if their *in-development* code passes all tests and gives good code coverage.

Travis works by reading _configurations_ from a repository's root directory called `.travis.yml` . The config file we use specifies two `stages` one for `frontend` and one for `backend`. Each stage has its own break-up of what commands need to be run `before_install`, for `install` and for testing (which can be controlled from `package.json` and `manage.py` respectively). Travis also allows us to run our builds on different versions of the core language or technology we are using (right now we just test on the version that we use in development).

The rest of the Travis config file is a sequention series of steps that need to be taken for each `stage` in the build. Reading through the config should be enough to make sense for any maintainer of this project.

You can see the latest build logs [here](https://travis-ci.com/github/mc-internship/covid19visualizer).

## Continuous Deployment Pipeline

This project will use a CD service called [Heroku](https://www.heroku.com). 

