# Usage

## Create .env file

```
cp .env.example .env
```

## HTTP

Simply run:

```
docker-compose up -d
```

And you are done! Your files from the `./data` directory are being served
at the `web-share.localhost` domain (if you haven't changed `.env` file).

## HTTPS (with certificate issued by Let's Encrypt)

If you are using [traefik-quick-start](https://github.com/lexuzieel/traefik-quick-start)
then bringing up an HTTPS version of web share is as trivial as:

```
docker-compose -f docker-compose.yml -f docker-compose.https.yml up -d
```

Do note, however, that by default this uses `staging-resolver` which will issue
[staging certificate](https://letsencrypt.org/docs/staging-environment/) and
will allow you to test your service before publishing it on the Internet.

Once you are ready to switch to a public facing domain, update `DOMAIN` in the 
`.env` file and set `CERT_RESOLVER` to `production-resolver`.

> There is currently a [bug with Traefik](https://github.com/traefik/traefik/issues/8633)
> that prevents switching between resolvers. If you have an already issued
> certificate by `staging-resolver` you first have to change `CERT_RESOLVER`
> parameter and restart the `web-share` project and then
> [remove acme.json file](https://github.com/lexuzieel/traefik-quick-start/blob/master/README.md#installation).
