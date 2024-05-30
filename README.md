```
 __  __    _ _ _         ____             _                        _
 \ \/ /___(_) (_) ___   | __ )  __ _  ___| | __      ___ _ __   __| |
  \  // __| | | |/ _ \  |  _ \ / _` |/ __| |/ /____ / _ \ '_ \ / _` |
  /  \\__ \ | | | (_) | | |_) | (_| | (__|   <_____|  __/ | | | (_| |
 /_/\_\___/_|_|_|\___/  |____/ \__,_|\___|_|\_\     \___|_| |_|\__,_|
```
# Xsilio Back-end
**Version**: 0.1
**Date**: June 2023
**Author**: Velocitech, Ltd.

Start Docker services (DB): `sudo docker-compose up -d`
Run the app: `npm run start:dev`

### Description
 Swagger documentation is available in /api endpoint.
 Staging BE https://staging.platform.xsilioplatform.com
 Production BE  https://production.platform.xsilioplatform.com 
 BE application was building using the following technologies 

*  Node.js with Typescript
 
 *  Nest.js framework
 
 *  Postgresql as database
 
 *  Typeorm os ORM

### Getting started 
   Before getting started please make sure you have the following programs and configuration set up
    <h4> Installing dependant programs </h4>
    
   *  Please install Postgresql for development or use remote Postgresql
   
   *  Please create database.\
       if you are running locally then need to provide all privileges to the user with commands below
       GRANT ALL ON SCHEMA public TO user\
       GRANT USAGE ON SCHEMA public TO user\
       GRANT ALL PRIVILEGES ON DATABASE database-name TO user
       
   *  Please install **node.js**
   
   *  Please install **npm**
   
   *  Please install **@nestjs/cli**
   
   *  Please install **PM2** 


### Setting up environmental dependency
  All environmental dependencies are in .env.example file so you have to provide values .
   1. To get all dependencies related to backblaze need to sign in or up  backblaze and get all environmental values related from there.

### Starting system and making it work
To add new users and create organsiations need to have System admin , who should be able to create Xsilio admins.
So starting point of application is creating System admin and then System admins .
System admins can be created manually. Not via endpoints. 

## Deployment information
Production and staging applications been deployed in AWS.
<h4> Applications </h4>
Applications are running in ec2 instances. EC2 instances configured by using AWS Bastion.A real application is running in a private EC2 instance and all the access is possible only by a public EC2 instance which acts as reverse proxy. In order to access it, you have to go by using public key
<h4> Database </h4>
Database in configured in AWS RDS
<h4> Backend images</h4>
Backend images are being upload into Backblaze

### Work with migrations:
- Create migration: `DB_HOST=localhost DB_TYPE=postgres DB_PORT=5432 DB_USERNAME=xsilio DB_PASSWORD=xsilio DB_NAME=xsilio npm run migration:generate -n MigrationName`
- Run migrations: `DB_HOST=localhost DB_TYPE=postgres DB_PORT=5432 DB_USERNAME=xsilio DB_PASSWORD=xsilio DB_NAME=xsilio npm run migration:up`


### Websocket
## Sockets.io are used.
- To connect to Sockets.io locally user `ws://localhost:3000`

- User *has* to provide token in **authorization** header to be able to connect!

Events user can connect to:
- `authentication` - Here user receive message if he is authenticated. Message will be in this format: `{"authenticated":true,"userId":"fb1712c1-5a7d-48ae-86cf-bb1793495d63"}` (Not necessary to be connected to)
- `connectedUsersCount` - Used to receive number of currently connected users to websockets server (Not necessary to be connected to)
- `chat` - For chat communication (*Necessary* to be connected to)
- `notifications` - Used for users to receive notifications. Notification will be received in this format: `data: { userId: string; notification: { title: string; content: string } }` (*Necessary* to be connected to)
