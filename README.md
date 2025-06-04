# Traefik ForwardAuth Example

This project demonstrates how to replace Nginx ingress with Traefik ingress, using Traefik's forwardAuth middleware along with a Flask authentication backend. This is a modification and adaptation of the original nginx-auth-request example.

## Original setup: （https://github.com/rickmak/nginx-auth-request）
The original project utilized Nginx's auth_request module to authenticate requests based on HTTP headers.

## New setup (this project):
This project replaces Nginx ingress with Traefik ingress, leveraging Traefik's built-in ForwardAuth middleware to perform authentication via an external Flask authentication service.


## How it works

1. The client sends requests to Nginx with or without the `x-pretest` header
2. Traefik forwards the authentication headers to the auth service
3. The auth service checks if the `x-pretest` header contains a valid token
4. If authentication succeeds, Nginx processes the request; otherwise, it returns a 401 error

## Valid Authentication

A valid request must include the header: `x-pretest: valid-token`

## Running the Demo

```bash
docker-compose up --build
```
![1](https://github.com/user-attachments/assets/704f3290-9c89-480c-be2a-df0964bfe9e6)

## Testing

You can test manually:

```bash
# Valid request
curl -H "x-pretest: valid-token" http://localhost:8080

# Invalid request
curl -H "x-pretest: wrong-token" http://localhost:8080

# Missing header
curl http://localhost:8080
```
![2](https://github.com/user-attachments/assets/54238a08-929e-4d6c-ac66-2a5eaa99aaae)
