# Installation \(On Local System\)

## Framework

This project uses [Feathers](http://feathersjs.com). An open source web framework for building modern real-time applications.

## Getting Started

> we recommand to install the project locally for the best development ease and performance

Getting up and running is as easy as 1, 2, 3, 4 ... 5.

1. Make sure you have [NodeJS](https://nodejs.org/), [yarn](https://yarnpkg.com), [mongoDB](https://www.mongodb.com/download-center#community) installed.

2. Clone this repo

   ```bash
   $ git clone https://github.com/Human-Connection/API.git
   ```

3. Install your dependencies

   ```bash
   $ cd ./API
   $ yarn
   ```

4. Setup local mailserver \(optional\)

   > **Note:**_You only have to start that mailserver when you want to register, reset your password or test emails in any form, it does not affect the rest of the application._

   Copy `config/local.example.json` to `config/local.json` and install the [MailDev](https://github.com/djfarrelly/MailDev) server to catch all sent emails in a nice web interface.

   ```bash
   # install mail dev (only has to be done once)
   $ npm install -g maildev

   # start the server, it will output the web url 
   # which normally is http://localhost:1080
   $ maildev
   ```

   You could also insert your smtp credentials into the local.json but that is not recommended as all emails would be sent to the given addresses which should not happen in development.

5. Start server

   Make sure that the `data` folder exists according to the `mongod --dbpath` in `package.json` to write the data into, then start the server:

   ```bash
   # start mongodb, feathers and seed database
   $ yarn dev
   $ yarn dev-win if you're on windows

   # start mongodb, feathers without seeding the database
   $ yarn dev-noseed

   # start mongodb, feathers for production
   $ yarn start
   ```

   > ##### IMPORTANT for WIN users:
   >
   > * make sure you have mongo bin directory added to your PATH
   > * if you picked another data directory during mongodb setup make sure to change package.json scripts section for key "dev-win" so it points to the proper path. Otherwise you will get missing data path errors from mongodb.

   If you did it right it will seed some fake data for you and downloads some images and avatar for faster development. Now you should be able to list some post at [http://localhost:3030/contributions](http://localhost:3030/contributions)

6. Setup and Start Thumbnail Service \(optional\)

   We are using [Thumbor](https://github.com/thumbor/thumbor) as a Thumbnail Microservice. You can install it locally if you like but this is totally optional.

   * At first you have to [install](http://thumbor.readthedocs.io/en/latest/installing.html) it locally.
   * After installation start it via the console with `thumbor`Set the `thumbor.url` in `config/local.json` to `http://localhost:8888`if not defined differently. The `thumbor.key` does not necessarily have to be defined, it just makes the URL more secure.

   > Do not forget to always start it if you choose that setup or otherwise you will not see any pictures at all.

## Local configuration

If you need to configure anything you can do so inside the `config/local.json` file. For that the `config/local.example.json` will contain always a minimal setup to get it working.

If, f.ex., you want to change listen address, port or URL, you can do so. Entries in the `config/local.json` will override entries in the `config/default.json`.

**Note on the seeder configuration** The seeder configuration has two properties:

* **dropDatabase:**
   drop the whole database on \(re\)start.
* **runOnInit:**
   run the seeder always on server \(re\)start \(when database is empty\).

> **Note**_You can switch the _`dropDatabase`_ entry after seeding and it will persist the seeded data._

## Testing

Simply run `yarn test` and all your tests in the `test/` directory will be run.

> **Note:**_At the moment there are some issues with linting while testing, but you can run the tests also with mocha run_

## Scaffolding

Feathers has a powerful command line interface. Here are a few things it can do:

```bash
$ npm install -g feathers-cli             
# Install Feathers CLI

$ feathers generate service               
# Generate a new Service

$ feathers generate hook                  
# Generate a new Hook

$ feathers generate model                 
# Generate a new Model

$ feathers help
# Show all commands
```



