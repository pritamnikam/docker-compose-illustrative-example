# docker-compose-illustrative-example
This example illustrates Compose specification concepts with a concrete example application.

Consider an application split into a frontend web application and a backend service.

The frontend is configured at runtime with an HTTP configuration file managed by infrastructure, providing an external domain name, and an HTTPS server certificate injected by the platform’s secured secret store.

The backend stores data in a persistent volume.

Both services communicate with each other on an isolated back-tier network, while frontend is also connected to a front-tier network and exposes port 443 for external usage.


(External user) --> 443 [frontend network]
                                |
                      +--------------------+
                      |  frontend service  |...ro...<HTTP configuration>
                      |      "webapp"      |...ro...<server certificate> #secured
                      +--------------------+
                                |
                        [backend network]
                                |
                      +--------------------+
                      |  backend service   |  r+w   ___________________
                      |     "database"     |=======( persistent volume )
                      +--------------------+        \_________________/


The example application is composed of the following parts:

- 2 services, backed by Docker images: webapp and database
- 1 secret (HTTPS certificate), injected into the frontend
- 1 configuration (HTTP), injected into the frontend
- 1 persistent volume, attached to the backend
- 2 networks
