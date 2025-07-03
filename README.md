# Spring Boot Security OAuth Example

#### Securing REST API with Spring Security OAuth2

## Running the Application

### Using Maven

1. Start the MySQL database using Docker Compose:
   ```
   docker-compose up -d
   ```

2. Run the Spring Boot application:
   ```
   mvn clean spring-boot:run
   ```

## Testing the Application

You can test the application using either Postman or curl commands.

### Using Postman

1. Generate a token:

    ![Authorization Tab](img/auth.png "Authorization Tab")

    ![Header Tab](img/header.png "Header Tab")

    ![Body Tab](img/body.png "Body Tab")

2. Accessing without Token:

    ![Accessing without Token](img/noauth.png "Accessing without Token")

3. Accessing Resource With Token:

    ![Accessing Resource with Token](img/oauth.png "Accessing Resource with Token")

### Using curl

1. Get an OAuth2 token using client credentials:
   ```
   curl -X POST \
     http://localhost:8080/oauth2/token \
     -H 'Authorization: Basic aGVuZGktY2xpZW50OmhlbmRpLXNlY3JldA==' \
     -H 'Content-Type: application/x-www-form-urlencoded' \
     -d 'grant_type=client_credentials&scope=read'
   ```
   Note: The Authorization header contains Base64 encoded `hendi-client:hendi-secret`

2. List all users (with token):
   ```
   curl -X GET \
     http://localhost:8080/users/user \
     -H 'Authorization: Bearer YOUR_ACCESS_TOKEN'
   ```

3. Create a new user (with token):
   ```
   curl -X POST \
     http://localhost:8080/users/user \
     -H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
     -H 'Content-Type: application/json' \
     -d '{
       "username": "newuser",
       "password": "password",
       "salary": 3000,
       "age": 25
     }'
   ```

4. Delete a user (with token):
   ```
   curl -X DELETE \
     http://localhost:8080/users/user/1 \
     -H 'Authorization: Bearer YOUR_ACCESS_TOKEN'
   ```

5. Try accessing without a token (will be denied):
   ```
   curl -X GET http://localhost:8080/users/user
   ```

## OAuth2 Configuration

- Client ID: `hendi-client`
- Client Secret: `hendi-secret`
- Grant Types: Authorization Code, Refresh Token, Client Credentials
- Access Token Validity: 1 hour
- Refresh Token Validity: 6 hours
