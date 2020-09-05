**Nginx connect() failed **- Connection refused while connecting to upstream
A small number of students are hitting an edge case where the nginx upstream connection is failing after they run docker-compose up --build:

connect() failed (111: Connection refused) while connecting to upstream, client:[DOCKER INTERNAL IP], server:, request: "GET / HTTP/1.1", upstream: [NETWORK IP]

The solution they found was to add this to their nginx service in the docker-compose.yml file:

  nginx:
    depends_on:
      - api
      - client


**Fix for "I Calculated Nothing Yet" message**
Hi!  Its entirely possible that you might run into a bug or two when you start up this set of containers with docker-compose.

Are you able to enter a number into the react app, but it appears to never be calculated, as seen in this screenshot?


If that's the case, then you can try adding in environment variables to the 'worker' entry in the docker-compose file, like so:

worker:
  environment:
    - REDIS_HOST=redis
    - REDIS_PORT=6379
Also, you can add depends_on to the api:

api:
  depends_on:
    - postgres
https://docs.docker.com/compose/compose-file/#depends_on

After any changes, make sure you run a docker-compose down and then docker-compose up --build

The next section also has a couple of other possible troubleshooting tips.