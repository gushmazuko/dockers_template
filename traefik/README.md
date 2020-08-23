
## [Traefik Basicauth](https://docs.traefik.io/middlewares/basicauth/)
* For Traefik basic authentication rename `docker-compose_basicauth.yml` to `docker-compose.yml`
* To create a `user:password` pair, the following command can be used:
```bash
echo $(htpasswd -nb user password) | sed -e s/\\$/\\$\\$/g
```
* Replace user password pair with your in `docker-compose.yml`
```yml
- "traefik.http.middlewares.${SERVICE}_auth.basicauth.users=user:$$apr1$$4h0uuN1U$$WAPb1/S2tWtrYtZwqS7Cp0"
```

## [Authelia Single Sign-On and Two-Factor](https://www.authelia.com/docs/deployment/supported-proxies/traefik2.x.html)
* For Authelia authentication rename `docker-compose_authelia.yml` to `docker-compose.yml`
* Uncomment `providers` directives in `traefik.toml`
```yml
[providers]
  [providers.file]
    directory = "/traefik_config"
    watch = true
```

## Environment Variables
* Replace values in `.env`
```
DOMAIN_NAME=site.mydomain.com
TZ=Europe/Berlin
```

* Replace `site.mydomain.com` in `traefik_config/dynamic_conf.toml`
```
    address = "http://authelia:9091/api/verify?rd=https://site.mydomain.com"
```