# Debug Static Web App CLI /w Custom Host and HTTPS

## **Static Web App does not handle proxying from HTTPS on port 4280 to the dev server running HTTPS on port 3000.**

See https://github.com/Azure/static-web-apps-cli/issues/600

This is a basic Create React App setup with a custom hostname and HTTPS using a
self signed certificate.

The `.env` file configure CRA to start with HTTPS and the hostname. e.g.
https://app.hostname.dev:3000

`.env`

```
HTTPS=true
HOST=app.hostname.dev
SSL_CRT_FILE=./ssl/dev-certificate.pem
SSL_KEY_FILE=./ssl/dev-key.pem
```

- Copy a self-signed certificate and key to the `ssl` folder.

Run `npm start` to prove that CRA works properly at
https://app.hostname.dev:3000 with a valid certificate.

`swa.cli.config.json`

```json
{
  "$schema": "https://aka.ms/azure/static-web-apps-cli/schema",
  "configurations": {
    "swa-ssl": {
      "appLocation": ".",
      "outputLocation": "build",
      "appBuildCommand": "npm run build",
      "ssl": true,
      "host": "app.hostname.dev",
      "sslCert": "./ssl/dev-certificate.pem",
      "sslKey": "./ssl/dev-key.pem",
      "run": "npm start",
      "appDevserverUrl": "https://app.hostname.dev:3000"
    }
  }
}
```
