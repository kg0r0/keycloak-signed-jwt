# keycloak-signed-jwt

Start keycloak with the following command. keycloak starts with the settings imported, so you don't need to do anything.

```
$ docker build . -t keycloak
$ docker run -p8080:8080 -it keycloak
```

Generate client_assertion and request token.

```
$ go run cmd/main.go
$ curl -s -X POST http://localhost:8080/realms/main/protocol/openid-connect/token \
 -H "Content-Type: application/x-www-form-urlencoded" \
 -d "client_id=sample-app" \
 -d "grant_type=client_credentials" \
 -d "scope=openid" \
 -d "client_assertion_type=urn:ietf:params:oauth:client-assertion-type:jwt-bearer" \
 -d "client_assertion=[CLIENT ASSERTION]"
```

## Setting Information

### master realm
| user name | password |
|-----------|----------|
| admin     | admin    |

### main realm

| client name |
|-------------|
| sample-app  |


The sample [keypair](key/key.json) is generated by [mkjwk](https://mkjwk.org/).