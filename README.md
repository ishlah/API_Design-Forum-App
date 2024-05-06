# Creat API Design Forum App

## Requirement/User Stories:

- As a user, I want to be able to Register
- As a user, I want to be able to Log In
- As a user, I want to be able to Create new Thread
- As a user, I want to be able to Create new Reply (on a Thread)
- As a user I want to be able to Update my Personal profile
- As a user, I want to be able to Save/Bookmark Threads
- As a user, I want to be able to UnSave/UnBM Threads
  
<img width="350" alt="drawSQL-image-export-2024-05-06" src="https://github.com/ishlah/API_Design-Forum-App/assets/108965733/9f262a0b-a026-49d6-912b-15b7f88d751a">

# Core Entity

## User
- id, fullName, userName, email, password, avatarUrl

## Thread
- id, title, category, content, userId

## Reply
- id, threadId, replyContent, userId

## Bookmark
- id, threadId, userId

# API Design

## Authentication

### Register

- Endpoint : **/api/auth/register**
- Method : **post**

- Request body :

  - fullName : string (required)
  - userName : string (required)
  - email : string (required)
  - password : string (required)
  - avatarUrl : string (optional)

- Response :

  - message : string
  - status : number

- Example Response :
  - Success : ```{message : "Registration successfully", status(201)}```
  - Conflic : ```{message : "Email already used", status(400)}```
  - Error : ```{message : "Registration error", status(500)}```

### Login

- Endpoint : **/api/auth/login**
- Method : **post**

- Request body :

  - email : string (required)
  - password : string (required)

- Response :

  - message : string
  - status : number

- Example Response :
  - Success : ```{message : "Login successfully", status(200)} ```
  - Error : ```{message : "Email or password invalid", status(401)}```
  - Error : ```{message : "Login error", status(500)} ```

## Thread

### Creat Thread

- Endpoint : **/api/threads**
- Method : **post**

- Request body :

  - title : string (required)
  - category : string (optional)
  - content : string (required)
  - userId : string(required) 

- Response :

  - message : string
  - status : number
  - data : object

- Example Response :
  - Success :
    ```
    {
    message : "Successfully creat new thread",
    status(201),
    data : {
    title : "Javascript vs Java",
    category : "technology",
    content : "lorem ipsum"
    userId : "user 1"}
    }
        
    ```
  - Error : ```{message : "error", status(500)}```
    
### Creat Reply

- Endpoint : **/api/replies**
- Method : **post**

- Request body :

  - threadId :string (required)
  - replyContent : string (required)
  - userId : string(required)

- Response :

  - message : string
  - status : number
  - data : object

- Example Response :
  - Success :
    ```
    {
    message : "Successfully creat new reply",
    status(201),
    data : {
    threadId : "Jago Javascript",
    replycontent : "lorem ipsum",
    userId : "user 2"}
    }

    ```
  - Error : ```{message : "error", status(500)}```

### Bookmarks

- Endpoint : **/api/bookmarks**
- Method : **post**

- Request body :

  - threadId : string(required)
  - userId : string (required)

- Response :

  - message : string
  - status : number
  - data : object

- Example Response :
  - Success :
    ```
    {
    message : "Successfully add bookmark",
    status(201),
    data : {
    threadId : "Api Design"
    userId: "user 2"}
    }

    ```
  - Error : ```{message : "error", status(500)}```

### Unbookmarks

- Endpoint : **/api/bookmarks/:id**
- Method : **delete**

- Request body :

  - id : string (required)

- Response :

  - message : string
  - status : number

- Example Response :
  - Success : ```{message : "Successfully remove bookmark", status(200)`}``
  - Error : ```{message : "error",status(500)}```

## User

### Update Profile

- Endpoint : **/api/users/:id**
- Method : **patch**

- Request body :

  - fullName : string (optional)
  - userName : string (optional)
  - email : string (optional)
  - password : string (optional)
  - avatarUrl : string (optional)

- Response :

  - message : string
  - status : number
  - data : object

- Example Response :
  - Success :
    ```
    {
    message : "Update profile successfully",
    status(200),
    data : {
    fullName : "mark clekc",
    userName : "mark_user",
    email : "mark@gmail.com",
    password : "12345",
    avatarUrl : "http://qwd43.png"}
    }

    ```
    
  - Error : ```{message : "error", status(500)}```

  

