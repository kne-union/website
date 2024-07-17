```shell
 docker network create kong-net

 docker run -d --name kong-database \
   --network=kong-net \
   -p 5432:5432 \
   -e "POSTGRES_USER=kong" \
   -e "POSTGRES_DB=kong" \
   -e "POSTGRES_PASSWORD=kongpass" \
   postgres:13

docker run -d --name kong-gateway \
 --network=kong-net \
 -e "KONG_DATABASE=postgres" \
 -e "KONG_PG_HOST=kong-database" \
 -e "KONG_PG_USER=kong" \
 -e "KONG_PG_PASSWORD=kongpass" \
 -e "KONG_PROXY_ACCESS_LOG=/dev/stdout" \
 -e "KONG_ADMIN_ACCESS_LOG=/dev/stdout" \
 -e "KONG_PROXY_ERROR_LOG=/dev/stderr" \
 -e "KONG_ADMIN_ERROR_LOG=/dev/stderr" \
 -e "KONG_ADMIN_LISTEN=0.0.0.0:8001" \
 -p 18000:8000 \
 -p 18001:8001 \
 kong/kong-gateway:3.7.1.2

docker run -d -p 18002:1337 \
            --network kong-net \
            --name konga \
            -e "NODE_ENV=production" \
            -e "TOKEN_SECRET=727e6193-d96b-4304-82f7-547445942936" \
            pantsel/konga
```
