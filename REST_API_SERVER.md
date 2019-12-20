# Simple REST API Server

## Guidelines

1. Codebase should be written in a Github repository.
2. Commits should follow the guidelines stated [here](https://github.com/angular/angular/blob/master/CONTRIBUTING.md#-commit-message-guidelines).
3. Project should be written in Typescript.
4. Source files should be in a separate directory named `src/` so that they can be isolated for building/compiling.
5. **Add tests for your project.** Test files should be in a separate directory named `test/`.
6. Project should include Typescript and ESLint config files.
7. Server should be built using [Koa module](https://www.npmjs.com/package/koa).
8. Database setup should be within docker.
9. Feel free to use appropriate and useful npm modules for your project.

## NPM Scripts

Here are the following `npm` commands you need to add:

1. `npm run docker` - runs the `docker-compose` command to setup database
2. `npm run lint` - runs the ESLint command to check for lint errors
3. `npm test` - runs the test files
4. `npm run build` - runs the Typescript build/compile command

## API Specifications

Here's the list of endpoints your simple REST API Server should support:

### 1. Create User

```
HTTP Method: POST
URL: /api/users
```

#### Request Body

- `email`\<string> - user's email
- `password`\<string> - user's password
- `name?`\<string> - user's name

```json
{
  "email": "input@email.com",
  "password": "password1"
}
```

#### Sample Response

```json
{
  "id": "e18faf18-8db0-4926-8fde-5ade9a22f254",
  "email": "input@email.com",
  "name": null
}
```

### 2. Authenticate User

```
HTTP Method: POST
URL: /api/auth
Headers:
  - Authorization: "Basic {encodedusername:password}"
```

#### Sample Response

```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJiZWQyZTM2Yy1mOWQ3LTRmNGMtYWVjNi0yNTY5YzhmMzFhNDMiLCJleHAiOjE1NzI0OTMzMzgsImlhdCI6MTU2OTkwMTMzOH0.a7_XGpPJfSS8OT5EGxmrhl3_bzOtx33TOZwQw3MHI8U"
}
```

### 3. Retrieve Single User

```
HTTP Method: GET
URL: /api/users/:id
Headers:
  - Authorization: "Bearer {token}"
```

#### Arguments

- `:id` - user's id

#### Sample Response

```json
{
  "id": "e18faf18-8db0-4926-8fde-5ade9a22f254",
  "email": "input@email.com",
  "name": null
}
```

### 4. Retrieve All Users

```
HTTP Method: GET
URL: /api/users
Headers:
  - Authorization: "Bearer {token}"
```

#### Sample Response

```json
[
  {
    "id": "e18faf18-8db0-4926-8fde-5ade9a22f254",
    "email": "input@email.com",
    "name": null
  }
]
```

### 5. Update Own Information

```
HTTP Method: PATCH
URL: /api/users
Headers:
  - Authorization: "Bearer {token}"
```

#### Request Body

- `name` - user's new name
- `password` - user's new password

```json
{
  "name": "new name",
  "password": "newpassword"
}
```

#### Sample Response

```json
{
  "id": "e18faf18-8db0-4926-8fde-5ade9a22f254",
  "email": "input@email.com",
  "name": "new name"
}
```
