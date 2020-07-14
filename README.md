# oauth2-proxy with ORY Hydra + Werther


This docker-compose file is basically a mixture of two docker-compose files. (from [oauth2-proxy](https://github.com/oauth2-proxy/oauth2-proxy) and [Werther](https://github.com/i-core/werther))

It brings up an instance of oauth2_proxy and hydra oauth/oidc provider for a quick demo.

Following services are involved in the whole chain
#### oauth2-proxy

A reverse proxy that provides authentication with Google, Github or other providers.
In our case it will authenticate with ORY Hydra.

#### nginx
Webserver hosting example static content that we want to protect.  oauth2_proxy will intercept any unauthenticated  request to web resource.

#### hydra
[ORY Hydra](https://www.ory.sh/)  is a hardened, OpenID Certified OAuth 2.0 Server and OpenID Connect Provider.
It is responsible for issuing access/userID tokens.

#### werther 
Werther is an Identity Provider for [ORY Hydra](https://www.ory.sh/) over [LDAP](https://ldap.com/). It implements [Login And Consent Flow](https://www.ory.sh/docs/hydra/oauth2) and provides basic UI.
When username/password is entered , it will check with the "ldap" service to see if the user is allowed to login.

#### hydra-client
Creates a oauth/oidc client for use with oauth2_proxy and then exits.

#### ldap

Acts as the ldap server and contains the  example user+password.



## How to run

- Clone the repo.
- Add the following hosts entries e.g) to your /etc/hosts
  ``` 
   127.0.0.1 oauth2-proxy.localhost
   127.0.0.1 oauth2-proxy.oauth2-proxy.localhost
   127.0.0.1 hydra.localhost
  ```
- Do
  ```docker-compose up```
- Initiate login flow
```  http://oauth2-proxy.localhost ```

- When prompted for login enter 
user ``` kolya_gerasyimov``` & password ```123```

You will be redirected to the static nginx welcome page.
