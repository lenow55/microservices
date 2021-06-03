# Microservices

A basic example of microservice architecture which demonstrates communication between a few loosely coupled services.

* Written in Go
* Uses RabbitMQ to communicate between services
* Uses WebSocket to talk to the front end
* Stores data in PostgreSQL
* Uses React for front end development
* Builds and runs the application with Docker

## Running the code

To run the example, clone the Github repository and start the services with Docker Compose. Once Docker finishes downloading and building images, the front end is accessible by visiting `localhost:8080` in a browser.

```bash
git clone https://github.com/ebosas/microservices
cd microservices
```
```bash
docker-compose up
```

### Back end

To access the back end service, attach to its docker container from a separate terminal window. Messages from the front end will show up here. Also, standart input from this service is sent to the front end for two way communication.

```bash
docker attach microservices_backend
```

### Database

To inspect the database, launch a new container that will connect to our Postgres database. Then enter the password `demopsw` (see the `.env` file).

```bash
docker run -it --rm --network microservices_network postgres:13-alpine psql -h postgres -U postgres
```

Select everything from the messages table:

```sql
\c microservices
select * from messages;
```

### RabbitMQ management

Access the RabbitMQ management interface by visiting `localhost:15672` with `guest` as both username and password.