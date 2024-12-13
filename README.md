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
    
    Step 2: Create a New Realm
    Once logged in, look at the top-left corner of the admin console, where you’ll see the current realm name (usually "Master" by default).
    
    Click the dropdown menu beside the realm name.
    
    Select Add realm from the dropdown.
    
    Step 3: Configure the New Realm
    In the Add Realm page:
    
    Realm Name: Enter a name for the realm (e.g., envoy-auth-realm).
    This name is case-sensitive and will be used in URLs.
    Click Create.
    
    step 4: Create a Client in Keycloak:
    
    In the created realm, go to Clients and create a new client:
    
    Client ID: envoy-client.
    Client Protocol: openid-connect.
    Access Type: confidential.
    Set the Redirect URI to the Envoy's address or service.   #give envoy-proxy external-ip here or if you uses ingress, and use envoy as ingress backend service. then use ingress domain here. like in my case (: http://envoy.disearch.ai/*)
    
    step 5: Configure Credentials:



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
