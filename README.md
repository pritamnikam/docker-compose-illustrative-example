# docker-compose-illustrative-example
This example illustrates Compose specification concepts with a concrete example application.

Consider an application split into a frontend web application and a backend service.

The frontend is configured at runtime with an HTTP configuration file managed by infrastructure, providing an external domain name, and an HTTPS server certificate injected by the platform’s secured secret store.

The backend stores data in a persistent volume.

Both services communicate with each other on an isolated back-tier network, while frontend is also connected to a front-tier network and exposes port 443 for external usage.


![image](https://github.com/pritamnikam/docker-compose-illustrative-example/blob/main/multi-container-illustrative-example.png)


The example application is composed of the following parts:

- 2 services, backed by Docker images: webapp and database
- 1 secret (HTTPS certificate), injected into the frontend
- 1 configuration (HTTP), injected into the frontend
- 1 persistent volume, attached to the backend
- 2 networks


This example illustrates the distinction between volumes, configs and secrets. While all of them are all exposed to service containers as mounted files or directories, only a volume can be configured for read+write access. Secrets and configs are read-only. The volume configuration allows you to select a volume driver and pass driver options to tweak volume management according to the actual infrastructure. Configs and Secrets rely on platform services, and are declared external as they are not managed as part of the application lifecycle: the Compose implementation will use a platform-specific lookup mechanism to retrieve runtime values.
