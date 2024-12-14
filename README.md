# To integrate Keycloak with Envoy Proxy for authentication and then forward requests to your backend (NGINX), you can follow these steps:

    1. Enable Keycloak Authentication
    Keycloak uses the OpenID Connect (OIDC) protocol for authentication. You’ll need to configure Keycloak as the identity provider.
    
    Steps:
    Create a Realm in Keycloak:
    
    Step 1: Access the Keycloak Admin Console
    Open your web browser and navigate to the Keycloak Admin Console URL.
    
    http://<keycloak-host>:8080/auth/
    Click on the Administration Console.
    
    Log in using your admin credentials:
    
    Username: admin
    Password: admin (or the password you configured).
    
    **link: https://docs.platformatic.dev/docs/next/guides/jwt-keycloak**

    follow this link for retrive token from keycloak.

    After configuring keycloak by following the link detail. In the last you need to use this command for retriving the key from keycloak. it correct. link ma jo command ma jo mention ha wo sahi ni ha..

    curl -L --insecure -s -X POST 'http://keycloak-development-service:8080/auth/realms/demorealm/protocol/openid-connect/token' \
    -H 'Content-Type: application/x-www-form-urlencoded' \
    --data-urlencode 'client_id=democlient' \
    --data-urlencode 'grant_type=client_credentials' \
    --data-urlencode 'client_secret=a48d18b9-6308-4e84-a585-c5dbecf9240b'

     

## command to get token key from keycloak

        curl -X POST "http://keycloak-development-service:8080/auth/realms/master/protocol/openid-connect/token"   -H "Content-Type: application/x-www-form-urlencoded"   -d "username=admin"   -d "password=RhNtAskong"   -d "grant_type=password"   -d "client_id=admin-cli""


    Navigate to the client > setting  and change **Access type** from **Public to Confidentail**.  and save it. It will open a new tab **Credential** adjust to the **Settings** under client.
    
    Navigate to the Credentials tab of the client.
    Note down the Client ID and Secret for later use.

## Command to get token using keycloak client information(working)
    
    curl -L --insecure -s -X POST 'http://keycloak-development-service:8080/auth/realms/demorealm/protocol/openid-connect/token' \
    -H 'Content-Type: application/x-www-form-urlencoded' \
    --data-urlencode 'client_id=democlient' \
    --data-urlencode 'grant_type=client_credentials' \
    --data-urlencode 'client_secret=a48d18b9-6308-4e84-a585-c5dbecf9240b'

## Command to send request along with token
    
    curl -X GET 'http://envoy.disearch.ai' \
    -H "Authorization: Bearer $access_token" \
    -H "Content-Type: application/json"
