## Dockerized cors proxy using nginx.

Meant for local development.

Proxy port is `1337`, if you don't like that, replace it using `search & replace` across this codebase.

Whenever you call `http://localhost:1337`, the call will get proxied to `http://${CORS_TARGET}:${CORS_TARGET_PORT}`

### Run using docker compose:

- Change ENV variables inside `docker-compose.yml`
- Run `docker compose up -d`

### Run without docker compose:

```
docker run \
  --name corsproxy \
  --hostname corsproxy \
  --restart no \
  --network bridge \
  -p 1337:80 \
  -e NGINX_PORT=80 \
  -e CORS_TARGET=host.docker.internal \
  -e CORS_TARGET_PORT=8080 \
  -v "$(pwd)/default.conf.template:/etc/nginx/templates/default.conf.template:ro" \
  --add-host host.docker.internal:host-gateway \
  nginx:alpine \
  nginx-debug -g "daemon off;"
```
